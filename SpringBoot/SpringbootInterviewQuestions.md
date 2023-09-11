## What is application context?
## What is Springboot annotation?
-  It combines multiple annotations, including @Configuration, @EnableAutoConfiguration, and @ComponentScan
## What is Springboot Autoconfiguration annotation?
- @EnableAutoConfiguration: Enables Spring Boot's auto-configuration feature, which automatically configures the application based on the dependencies on the classpath.
## What is @Profile Annotation?
- @Profile: Specifies which beans should be active or inactive based on the active Spring profiles.

## What is Conditional Annotation?
- In Spring Framework, the @Conditional annotation is used to conditionally include or exclude a bean's configuration based on certain conditions. `These conditions are typically evaluated at runtime`, allowing you to dynamically configure your application based on various criteria
## What is ConditionalOnClass, ConditionalOnProperty, and ConditionalOnBean?
- @ConditionalOnBean: This annotation lets you include a bean configuration if a specified bean or beans are already defined in the application context. It's useful for creating beans that depend on the existence of other beans.
- @ConditionalOnMissingBean: Similar to @ConditionalOnBean, this annotation includes a bean configuration only if a specified bean or beans are not defined in the application context.
- @ConditionalOnClass: This annotation allows you to conditionally include a bean configuration if a specified class or classes are present on the classpath. For example, you can use it to configure a bean only if a particular library or class is available.
- @ConditionalOnResource: Conditionally include a bean configuration if a specified resource (file, classpath resource, etc.) exists. This is useful for configuring beans that depend on external resources.

## What is Springboot.run() method?
- SpringApplication that contains this static method called run().
- Peforms Various Tasks:
    - Sets up the initial configuration.
    - Starts the Application Context of Spring.
    - Scans Class Path
    - Downloads and starts Tomcat Server.
## How to change the port number?
- Command Line
    ```plaintext
    java -jar spring-5.jar --server.port=8083
    ```

- Application Properties
- Configuration
```java
@SpringBootApplication
public class CustomApplication {
public static void main(String[] args {
SpringApplication app = new SpringApplication(CustomApplication.class);
app.setDefaultProperties(Collection.singletonMap("server.port", "8083"));
app.run(args);
}
```
## How to change the profile in springboot?
## What is the difference in restcontroller and controller?
## What is RestController Annotation?
- @RestController is a specialized version of the controller. It includes the @Controller and @ResponseBody annotations, and as a result, simplifies the controller implementation:
## What is ResponseBody annotation?
- Purpose: The primary purpose of @ResponseBody is to tell Spring that the return value of the annotated method should be sent as the response content (usually in JSON, XML, or other formats) rather than being resolved as a view to render.
- Usage: You can apply @ResponseBody at the method level or at the class level (on the controller class) to indicate that all handler methods in the class should have their return values serialized to the response body.
- Return Types: Common return types for methods annotated with @ResponseBody include Java objects, collections, or ResponseEntity instances. Spring will use a message converter to serialize the return value to the appropriate format based on the Accept header of the HTTP request.
```java 
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;

@Controller
public class MyController {

    @RequestMapping("/hello")
    @ResponseBody
    public String hello() {
        return "Hello, World!";
    }
}
```


## What is GetMapping?
## What are Springboot starter poms?
## Why Springboot over Spring?

## What is PostConstruct Annotation?
## What is IOC Container?
## What is depedency Injection?
## What is Springboot actuator?
- Spring Actuator is a cool feature of Spring Boot with the help of which you can see what is happening inside a running application.
- The Spring Actuator provides a very easy way to access the production-ready REST points and fetch all kinds of information from the web. These points are secured using Spring Security’s content negotiation strategy.
## How to change the embedded web server?
## What is setter injection?
## What is constructor injection?
## What is Request params?
## What is the difference in Log4j2 and Log4j?
- Log4j2 comes with many features that Log4j didn't have. Similarly, Log4j only supported configuration files in properties and XML formats, while Log4j2 supports configuration through XML, JSON, YAML, and configuration files/programmatic actions
## Can you explain how to deploy to a different server with Spring Boot?
- To deploy a different server with Spring Boot, follow the below steps:
    -   Generate a WAR from the project
    -   Then, deploy the WAR file onto your favorite server
## What is Component Scan Annotation?
## What is SpringBoot CLI?
## How to create war file in spring boot?
- To create a war file in spring boot you need to define your packaging file as war in your pom.xml(if it is maven project).
- Then just do maven clean and install so that your application will start building. Once the build is successful, just go into your Target folder and you can see .war file generated for your application.  