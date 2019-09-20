# json-xml-support
SpringBoot microservice which supports both xml and json media type

# Steps to follow :

1. Add dependencies in the pom.xml for the xml support.
    
```aidl
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
    <version>2.9.0</version>
</dependency>
```
    
2.  Add the configuration code as below.

There are 3 ways in which we can send a request for the mediaType response of our interest.

a. Path Extentions
b. Parameters
c. Headers

Path Extensions have higher priorities over Parameters and Headers.
Parameters have higher priorities over Headers.
Headers have lowest priorities.

```aidl
import org.springframework.context.annotation.Configuration;
import org.springframework.http.MediaType;
import org.springframework.web.servlet.config.annotation.ContentNegotiationConfigurer;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurer;

@Configuration
@EnableWebMvc
public class JsonXmlSupportConfiguration implements WebMvcConfigurer {

    @Override
    public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
        configurer
                .favorPathExtension(true)
                .favorParameter(true)
                .parameterName("mediaType")
                .ignoreAcceptHeader(false)
                .defaultContentType(MediaType.APPLICATION_JSON)
                .mediaType("xml",MediaType.APPLICATION_XML)
                .mediaType("json",MediaType.APPLICATION_JSON);
    }
}
```

3. import JsonXmlSupport.postman_collection.json in postman collection and test the apis.

# Test 1

Request
```aidl
http://localhost:8080/employees.xml
```
Response
```aidl
<List>
    <item>
        <firstName>Suraj</firstName>
        <middleName>Panduranga</middleName>
        <lastName>Jannu</lastName>
        <age>26</age>
        <salary>100000.0</salary>
    </item>
    <item>
        <firstName>Pramod</firstName>
        <middleName>Panduranga</middleName>
        <lastName>Jannu</lastName>
        <age>29</age>
        <salary>300000.0</salary>
    </item>
    <item>
        <firstName>Mohan</firstName>
        <middleName/>
        <lastName>Mari</lastName>
        <age>49</age>
        <salary>200000.0</salary>
    </item>
    <item>
        <firstName>Abhilash</firstName>
        <middleName/>
        <lastName>Jayaswami</lastName>
        <age>34</age>
        <salary>400000.0</salary>
    </item>
    <item>
        <firstName>Harsha</firstName>
        <middleName/>
        <lastName/>
        <age>28</age>
        <salary>500000.0</salary>
    </item>
    <item>
        <firstName>Imran</firstName>
        <middleName>R</middleName>
        <lastName>H</lastName>
        <age>26</age>
        <salary>800000.0</salary>
    </item>
</List>
```

# Test 2

Request
```aidl
http://localhost:8080/employees.json
```
Response
```aidl
[
    {
        "firstName": "Suraj",
        "middleName": "Panduranga",
        "lastName": "Jannu",
        "age": 26,
        "salary": 100000
    },
    {
        "firstName": "Pramod",
        "middleName": "Panduranga",
        "lastName": "Jannu",
        "age": 29,
        "salary": 300000
    },
    {
        "firstName": "Mohan",
        "middleName": null,
        "lastName": "Mari",
        "age": 49,
        "salary": 200000
    },
    {
        "firstName": "Abhilash",
        "middleName": null,
        "lastName": "Jayaswami",
        "age": 34,
        "salary": 400000
    },
    {
        "firstName": "Harsha",
        "middleName": null,
        "lastName": null,
        "age": 28,
        "salary": 500000
    },
    {
        "firstName": "Imran",
        "middleName": "R",
        "lastName": "H",
        "age": 26,
        "salary": 800000
    }
]
```

# Test 3

Request
```aidl
http://localhost:8080/employees?mediaType=xml
```
Response
```aidl
<List>
    <item>
        <firstName>Suraj</firstName>
        <middleName>Panduranga</middleName>
        <lastName>Jannu</lastName>
        <age>26</age>
        <salary>100000.0</salary>
    </item>
    <item>
        <firstName>Pramod</firstName>
        <middleName>Panduranga</middleName>
        <lastName>Jannu</lastName>
        <age>29</age>
        <salary>300000.0</salary>
    </item>
    <item>
        <firstName>Mohan</firstName>
        <middleName/>
        <lastName>Mari</lastName>
        <age>49</age>
        <salary>200000.0</salary>
    </item>
    <item>
        <firstName>Abhilash</firstName>
        <middleName/>
        <lastName>Jayaswami</lastName>
        <age>34</age>
        <salary>400000.0</salary>
    </item>
    <item>
        <firstName>Harsha</firstName>
        <middleName/>
        <lastName/>
        <age>28</age>
        <salary>500000.0</salary>
    </item>
    <item>
        <firstName>Imran</firstName>
        <middleName>R</middleName>
        <lastName>H</lastName>
        <age>26</age>
        <salary>800000.0</salary>
    </item>
</List>
```

# Test 4

Request
```aidl
http://localhost:8080/employees?mediaType=json
```
Response
```aidl
[
    {
        "firstName": "Suraj",
        "middleName": "Panduranga",
        "lastName": "Jannu",
        "age": 26,
        "salary": 100000
    },
    {
        "firstName": "Pramod",
        "middleName": "Panduranga",
        "lastName": "Jannu",
        "age": 29,
        "salary": 300000
    },
    {
        "firstName": "Mohan",
        "middleName": null,
        "lastName": "Mari",
        "age": 49,
        "salary": 200000
    },
    {
        "firstName": "Abhilash",
        "middleName": null,
        "lastName": "Jayaswami",
        "age": 34,
        "salary": 400000
    },
    {
        "firstName": "Harsha",
        "middleName": null,
        "lastName": null,
        "age": 28,
        "salary": 500000
    },
    {
        "firstName": "Imran",
        "middleName": "R",
        "lastName": "H",
        "age": 26,
        "salary": 800000
    }
]
```

# Test 5

Request
```aidl
http://localhost:8080/employees
```
Headers
```aidl
Accept : application/xml
```
Response
```aidl
<List>
    <item>
        <firstName>Suraj</firstName>
        <middleName>Panduranga</middleName>
        <lastName>Jannu</lastName>
        <age>26</age>
        <salary>100000.0</salary>
    </item>
    <item>
        <firstName>Pramod</firstName>
        <middleName>Panduranga</middleName>
        <lastName>Jannu</lastName>
        <age>29</age>
        <salary>300000.0</salary>
    </item>
    <item>
        <firstName>Mohan</firstName>
        <middleName/>
        <lastName>Mari</lastName>
        <age>49</age>
        <salary>200000.0</salary>
    </item>
    <item>
        <firstName>Abhilash</firstName>
        <middleName/>
        <lastName>Jayaswami</lastName>
        <age>34</age>
        <salary>400000.0</salary>
    </item>
    <item>
        <firstName>Harsha</firstName>
        <middleName/>
        <lastName/>
        <age>28</age>
        <salary>500000.0</salary>
    </item>
    <item>
        <firstName>Imran</firstName>
        <middleName>R</middleName>
        <lastName>H</lastName>
        <age>26</age>
        <salary>800000.0</salary>
    </item>
</List>
```

# Test 6

Request
```aidl
http://localhost:8080/employees
```
Headers
```aidl
Accept : application/json
```
Response
```aidl
[
    {
        "firstName": "Suraj",
        "middleName": "Panduranga",
        "lastName": "Jannu",
        "age": 26,
        "salary": 100000
    },
    {
        "firstName": "Pramod",
        "middleName": "Panduranga",
        "lastName": "Jannu",
        "age": 29,
        "salary": 300000
    },
    {
        "firstName": "Mohan",
        "middleName": null,
        "lastName": "Mari",
        "age": 49,
        "salary": 200000
    },
    {
        "firstName": "Abhilash",
        "middleName": null,
        "lastName": "Jayaswami",
        "age": 34,
        "salary": 400000
    },
    {
        "firstName": "Harsha",
        "middleName": null,
        "lastName": null,
        "age": 28,
        "salary": 500000
    },
    {
        "firstName": "Imran",
        "middleName": "R",
        "lastName": "H",
        "age": 26,
        "salary": 800000
    }
]
```

# Test 7

Request
```aidl
http://localhost:8080/employees.xml?mediaType=json
```
Response
```aidl
<List>
    <item>
        <firstName>Suraj</firstName>
        <middleName>Panduranga</middleName>
        <lastName>Jannu</lastName>
        <age>26</age>
        <salary>100000.0</salary>
    </item>
    <item>
        <firstName>Pramod</firstName>
        <middleName>Panduranga</middleName>
        <lastName>Jannu</lastName>
        <age>29</age>
        <salary>300000.0</salary>
    </item>
    <item>
        <firstName>Mohan</firstName>
        <middleName/>
        <lastName>Mari</lastName>
        <age>49</age>
        <salary>200000.0</salary>
    </item>
    <item>
        <firstName>Abhilash</firstName>
        <middleName/>
        <lastName>Jayaswami</lastName>
        <age>34</age>
        <salary>400000.0</salary>
    </item>
    <item>
        <firstName>Harsha</firstName>
        <middleName/>
        <lastName/>
        <age>28</age>
        <salary>500000.0</salary>
    </item>
    <item>
        <firstName>Imran</firstName>
        <middleName>R</middleName>
        <lastName>H</lastName>
        <age>26</age>
        <salary>800000.0</salary>
    </item>
</List>
```

# Test 8

Request
```aidl
http://localhost:8080/employees?mediaType=json
```
Headers
```aidl
Accept : application/xml
```
Response
```aidl
[
    {
        "firstName": "Suraj",
        "middleName": "Panduranga",
        "lastName": "Jannu",
        "age": 26,
        "salary": 100000
    },
    {
        "firstName": "Pramod",
        "middleName": "Panduranga",
        "lastName": "Jannu",
        "age": 29,
        "salary": 300000
    },
    {
        "firstName": "Mohan",
        "middleName": null,
        "lastName": "Mari",
        "age": 49,
        "salary": 200000
    },
    {
        "firstName": "Abhilash",
        "middleName": null,
        "lastName": "Jayaswami",
        "age": 34,
        "salary": 400000
    },
    {
        "firstName": "Harsha",
        "middleName": null,
        "lastName": null,
        "age": 28,
        "salary": 500000
    },
    {
        "firstName": "Imran",
        "middleName": "R",
        "lastName": "H",
        "age": 26,
        "salary": 800000
    }
]
```

# Test 9

Request
```aidl

```
Response
```aidl

```


