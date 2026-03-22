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
