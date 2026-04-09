# SERVICE
```java
import com.opencsv.bean.CsvToBeanBuilder;
import org.springframework.stereotype.Service;

import java.io.FileReader;
import java.util.List;

@Service
public class CSVService {

    public List<User> readCSV(String filePath) {

        try {
        //List<User> user = ...
            return new CsvToBeanBuilder<User>(new FileReader(filePath))
                    .withType(User.class)
                    .withIgnoreLeadingWhiteSpace(true)
                    .build()
                    .parse();

        } catch (Exception e) {
            e.printStackTrace();
        }

        return null;
    }
}


```

📄 XMLToJSONService.java
```java
package com.example.demo.service;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.dataformat.xml.XmlMapper;
import org.springframework.stereotype.Service;

@Service
public class XMLToJSONService {

    public String convert(String xml) {

        try {
            XmlMapper xmlMapper = new XmlMapper();
            Object obj = xmlMapper.readValue(xml, Object.class);

            ObjectMapper jsonMapper = new ObjectMapper();
            return jsonMapper.writerWithDefaultPrettyPrinter()
                    .writeValueAsString(obj);

        } catch (Exception e) {
            e.printStackTrace();
        }

        return "Error converting XML";
    }
}
```

Alright — this is a **real backend project (and a strong one for your resume)** 🔥

Let’s break it into a **clear, do-able plan** so you can actually build it step by step.

---

# **🧠 What you’re building**

  

👉 A system that:

1. Fetches CVE data from NVD API
    
2. Stores it in DB
    
3. Exposes APIs to query it
    

---

# **🏗️ Tech Stack (recommended)**

  

Since you’re already using Spring Boot:

- ✅ Spring Boot (REST API)
    
- ✅ MongoDB (best for JSON data)
    
- ✅ WebClient / RestTemplate (API calls)
    

---

# **🚀 STEP-BY-STEP IMPLEMENTATION**

---

# **🧱 STEP 1: Create Spring Boot Project**

  

Dependencies:

```
Spring Web
Spring Data MongoDB
Lombok (optional)
```

---

# **🌐 STEP 2: Understand NVD API**

  

Base URL:

```
https://services.nvd.nist.gov/rest/json/cves/2.0
```

Pagination params:

```
startIndex=0
resultsPerPage=2000
```

---

# **📦 STEP 3: Create Model (CVE Entity)**

  

📄 CVE.java

```
package com.example.cve.model;

import lombok.Data;
import org.springframework.data.annotation.Id;
import org.springframework.data.mongodb.core.mapping.Document;

@Data
@Document(collection = "cves")
public class CVE {

    @Id
    private String id; // CVE ID

    private String sourceIdentifier;
    private String published;
    private String lastModified;

    private String description;
}
```

---

# **🗄️ STEP 4: Repository**

```
package com.example.cve.repository;

import com.example.cve.model.CVE;
import org.springframework.data.mongodb.repository.MongoRepository;

import java.util.List;

public interface CVERepository extends MongoRepository<CVE, String> {

    List<CVE> findByLastModifiedAfter(String date);
}
```

---

# **🌍 STEP 5: Service (Fetch + Store)**

  

📄 CVEFetchService.java

```java
package com.example.cve.service;

import com.example.cve.model.CVE;
import com.example.cve.repository.CVERepository;
import org.json.JSONArray;
import org.json.JSONObject;
import org.springframework.stereotype.Service;
import org.springframework.web.client.RestTemplate;

@Service
public class CVEFetchService {

    private final CVERepository repo;
    private final RestTemplate restTemplate = new RestTemplate();

    public CVEFetchService(CVERepository repo) {
        this.repo = repo;
    }

    public void fetchAndStore() {
        int startIndex = 0;
        int pageSize = 2000;

        while (true) {

            String url = "https://services.nvd.nist.gov/rest/json/cves/2.0?startIndex="
                    + startIndex + "&resultsPerPage=" + pageSize;

            String response = restTemplate.getForObject(url, String.class);
            JSONObject json = new JSONObject(response);

            JSONArray vulnerabilities = json.getJSONArray("vulnerabilities");

            if (vulnerabilities.length() == 0) break;

            for (int i = 0; i < vulnerabilities.length(); i++) {
                JSONObject cveObj = vulnerabilities.getJSONObject(i).getJSONObject("cve");

                CVE cve = new CVE();
                cve.setId(cveObj.getString("id"));
                cve.setSourceIdentifier(cveObj.optString("sourceIdentifier"));
                cve.setPublished(cveObj.optString("published"));
                cve.setLastModified(cveObj.optString("lastModified"));

                // description
                String desc = cveObj.getJSONObject("descriptions")
                        .getJSONArray("description_data")
                        .getJSONObject(0)
                        .getString("value");

                cve.setDescription(desc);

                repo.save(cve);
            }

            startIndex += pageSize;
        }
    }
}
```

---

# **🔎 STEP 6: Query Service**

  

📄 CVEService.java

```java
package com.example.cve.service;

import com.example.cve.model.CVE;
import com.example.cve.repository.CVERepository;
import org.springframework.stereotype.Service;

import java.time.LocalDateTime;
import java.util.List;

@Service
public class CVEService {

    private final CVERepository repo;

    public CVEService(CVERepository repo) {
        this.repo = repo;
    }

    public CVE getById(String id) {
        return repo.findById(id).orElse(null);
    }

    public List<CVE> getRecent(int days) {
        LocalDateTime date = LocalDateTime.now().minusDays(days);
        return repo.findByLastModifiedAfter(date.toString());
    }
}
```

---

# **🌐 STEP 7: Controller**

  

📄 CVEController.java

```java
package com.example.cve.controller;

import com.example.cve.model.CVE;
import com.example.cve.service.CVEFetchService;
import com.example.cve.service.CVEService;
import org.springframework.web.bind.annotation.*;

import java.util.List;

@RestController
@RequestMapping("/cve")
public class CVEController {

    private final CVEService service;
    private final CVEFetchService fetchService;

    public CVEController(CVEService service, CVEFetchService fetchService) {
        this.service = service;
        this.fetchService = fetchService;
    }

    // fetch all CVEs
    @GetMapping("/fetch")
    public String fetchData() {
        fetchService.fetchAndStore();
        return "Data fetched and stored!";
    }

    // get by ID
    @GetMapping("/{id}")
    public CVE getById(@PathVariable String id) {
        return service.getById(id);
    }

    // get by last modified days
    @GetMapping("/recent/{days}")
    public List<CVE> getRecent(@PathVariable int days) {
        return service.getRecent(days);
    }
}
```

---

# **⚙️ STEP 8: application.properties**

```
spring.data.mongodb.uri=mongodb://localhost:27017/cvedb
```

---

# **🧪 STEP 9: Test APIs**

  

### **1️⃣ Fetch data**

```
GET /cve/fetch
```

---

### **2️⃣ Get by ID**

```
GET /cve/CVE-2021-34527
```

---

### **3️⃣ Get recent**

```
GET /cve/recent/7
```

---

# **⚠️ Important Improvements (VERY IMPORTANT)**

  

## **🔥 1. Add delay (API rate limit)**

```
Thread.sleep(6000);
```

---

## **🔥 2. Use pagination safely**

- NVD API has limits
    
- Don’t spam requests
    

---

## **🔥 3. Store only required fields**

  

Otherwise DB becomes huge

---

# **🧠 Architecture Summary**

```
Controller → Service → Repository → MongoDB
                    ↑
                External API
```

---

# **💥 What you just built**

  

👉 This is:

- Real-world backend system
    
- Data ingestion pipeline
    
- REST API system
    

---

# **🚀 If you want next**

  

I can help you:

- Add Swagger UI 🔥
    
- Optimize DB schema
    
- Add caching (Redis)
    
- Deploy this project
    

  

Just tell me 👍

Perfect — I’ll give you a **clean, complete Spring Boot version (Service + Controller)** that you can directly run 🔥

---

# **🧠 What this includes**

- ✅ JSON → XML conversion (as per your spec)
    
- ✅ REST API (POST /convert)
    
- ✅ Proper XML response header
    
- ✅ Clean structure
    

---

# **📦 1. Service Class**

  

📄 JSONToXMLService.java

```
package com.example.demo.service;

import org.json.*;
import org.springframework.stereotype.Service;

@Service
public class JSONToXMLService {

    public String convert(String jsonText) {
        Object json = new JSONTokener(jsonText).nextValue();

        if (json instanceof JSONObject) {
            return convertObject((JSONObject) json);
        } else if (json instanceof JSONArray) {
            return convertArray((JSONArray) json);
        }

        return "";
    }

    private String convertValue(Object value, String name) {
        if (value == JSONObject.NULL) {
            return "<null/>";
        } else if (value instanceof String) {
            return buildTag("string", name, value.toString());
        } else if (value instanceof Number) {
            return buildTag("number", name, value.toString());
        } else if (value instanceof Boolean) {
            return buildTag("boolean", name, value.toString());
        } else if (value instanceof JSONObject) {
            return convertObject((JSONObject) value, name);
        } else if (value instanceof JSONArray) {
            return convertArray((JSONArray) value, name);
        }
        return "";
    }

    private String buildTag(String type, String name, String value) {
        if (name != null) {
            return "<" + type + " name=\"" + name + "\">" + value + "</" + type + ">";
        } else {
            return "<" + type + ">" + value + "</" + type + ">";
        }
    }

    private String convertObject(JSONObject obj) {
        return convertObject(obj, null);
    }

    private String convertObject(JSONObject obj, String name) {
        StringBuilder xml = new StringBuilder();

        if (name != null)
            xml.append("<object name=\"").append(name).append("\">");
        else
            xml.append("<object>");

        for (String key : obj.keySet()) {
            xml.append(convertValue(obj.get(key), key));
        }

        xml.append("</object>");
        return xml.toString();
    }

    private String convertArray(JSONArray arr) {
        return convertArray(arr, null);
    }

    private String convertArray(JSONArray arr, String name) {
        StringBuilder xml = new StringBuilder();

        if (name != null)
            xml.append("<array name=\"").append(name).append("\">");
        else
            xml.append("<array>");

        for (int i = 0; i < arr.length(); i++) {
            xml.append(convertValue(arr.get(i), null));
        }

        xml.append("</array>");
        return xml.toString();
    }
}
```

---

# **🌐 2. Controller Class**

  

📄 ConverterController.java

```
package com.example.demo.controller;

import com.example.demo.service.JSONToXMLService;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/convert")
public class ConverterController {

    private final JSONToXMLService service;

    public ConverterController(JSONToXMLService service) {
        this.service = service;
    }

    @PostMapping
    public ResponseEntity<String> convertJSON(@RequestBody String json) {

        String xml = service.convert(json);

        return ResponseEntity
                .ok()
                .header("Content-Type", "application/xml")
                .body(xml);
    }
}
```

---

# **▶️ 3. Run the App**

```
mvn spring-boot:run
```

---

# **🧪 4. Test API**

  

### **Endpoint:**

```
POST http://localhost:8080/convert
```

---

### **Body (JSON):**

```
{
  "name": "Raj",
  "age": 21,
  "skills": ["Java", "Python"],
  "isStudent": true
}
```

---

### **Response (XML):**

```
<object>
<string name="name">Raj</string>
<number name="age">21</number>
<array name="skills">
<string>Java</string>
<string>Python</string>
</array>
<boolean name="isStudent">true</boolean>
</object>
```

---

# **🔥 Bonus (Optional Improvement)**

  

If you want **pretty formatted XML**, I can upgrade this to:

```
<object>
  <string name="name">Raj</string>
  ...
</object>
```

---

# **⚡ Important Reminder**

  

👉 Use this **for learning / demo / portfolio**

👉 Submit **CLI version** for assignment (safe side)

---

# **👍 If you want next**

  

I can help you:

- Add Swagger UI 🔥
    
- Add file upload API
    
- Convert this into **production-level clean architecture**
    

  

Just tell me 👍