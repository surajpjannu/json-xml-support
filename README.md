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