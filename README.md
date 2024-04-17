# springboot-swagger-doc
Sample springboot Swagger Doc Project Using Open Api Doc

# springboot-swagger-doc
Sample springboot Swagger Doc Project Using Open Api Doc

Link : https://www.baeldung.com/spring-rest-openapi-documentation

Dependeacies mainly for Services for Swagger open api enabling 

 <!-- swagger dependency -->
        <dependency>
            <groupId>org.springdoc</groupId>
            <artifactId>springdoc-openapi-starter-webmvc-ui</artifactId>
            <version>2.5.0</version>
        </dependency>
        <dependency>
            <groupId>org.springdoc</groupId>
            <artifactId>springdoc-openapi-starter-common</artifactId>
            <version>2.5.0</version>
        </dependency>

Codes to be added in services Sample

<!-- swagger dependency -->
```java
import io.swagger.v3.oas.annotations.OpenAPIDefinition;
import io.swagger.v3.oas.annotations.enums.SecuritySchemeIn;
import io.swagger.v3.oas.annotations.enums.SecuritySchemeType;
import io.swagger.v3.oas.annotations.info.Contact;
import io.swagger.v3.oas.annotations.info.Info;
import io.swagger.v3.oas.annotations.security.SecurityScheme;
import io.swagger.v3.oas.annotations.security.SecuritySchemes;
import io.swagger.v3.oas.annotations.servers.Server;
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.cloud.client.discovery.EnableDiscoveryClient;
import org.springframework.cloud.openfeign.EnableFeignClients;

@SpringBootApplication
@EnableDiscoveryClient
@EnableFeignClients
@OpenAPIDefinition(
        info = @Info(
                title = "Sample Service",
                version = "1.0.0",
                description = "",
                contact = @Contact(name = "Sample Service", email = "emailId", url = "Any Url")
        ),
        servers = {@Server(url = "Server Url")}
)
@SecuritySchemes({
        @SecurityScheme(type = SecuritySchemeType.HTTP,
                name = "bearerAuth",
                in = SecuritySchemeIn.HEADER,
                bearerFormat = "jwt",
                scheme = "bearer"
        )
})
public class SampleService {
    public static void main(String[] args) {
        SpringApplication.run(SampleService.class, args);
    }
}

Application Properties to be Added in the service not swagger api document project
Note: According to the context path of the project it will work .
Note: Allow it in spring security config and filters , because it does not need any validation
springdoc.api-docs.path=/api/v1/api-docs

```

```java 
##Properties

Application Properties to be Added Swagger Documentation Project
sampleswaggerdoc.serviceOneUrl=${SERVICE_ONE_URL:http://localhost:8080}/contextpath1/api/v1/api-docs
sampleswaggerdoc.serviceTwoUrl=${SERVICE_TWO_URL:http://localhost:8083}/contextpath2/api/v1/api-docs
sampleswaggerdoc.serviceThreeUrl=${SERVICE_THREE_URL:http://localhost:8070}/contextpath3/api/v1/api-docs

springdoc.swagger-ui.path=/
springdoc.swagger-ui.urls[0].url= /service-one-docs
springdoc.swagger-ui.urls[0].name=Service One
springdoc.swagger-ui.urls[1].url= /crm-docs
springdoc.swagger-ui.urls[1].name=Service Two
springdoc.swagger-ui.urls[2].url= /service-two-docs
springdoc.swagger-ui.urls[2].name=Service Three
springdoc.swagger-ui.urls[3].url= /service-three-docs




