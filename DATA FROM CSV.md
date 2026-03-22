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



