# gae-standard-example

 # This is a hello world basic spring boot application added to GCP app engine
 
 https://codelabs.developers.google.com/codelabs/cloud-app-engine-springboot/index.html
 
$ curl https://start.spring.io/starter.tgz -d packaging=war \
  -d dependencies=web -d baseDir=gae-standard-example | tar -xzvf -
$ cd gae-standard-example

<build>
    <plugins>
      ...
      <plugin>
        <groupId>com.google.cloud.tools</groupId>
        <artifactId>appengine-maven-plugin</artifactId>
        <version>1.3.2</version>
        <configuration>
          <version>1</version>
        </configuration>
      </plugin>
      ...
    </plugins>
  </build>
  
$ mkdir -p src/main/webapp/WEB-INF/
$ touch src/main/webapp/WEB-INF/appengine-web.xml

 <appengine-web-app xmlns="http://appengine.google.com/ns/1.0">
  <threadsafe>true</threadsafe>
  <runtime>java8</runtime>
</appengine-web-app>
 
@SpringBootApplication
@RestController
public class DemoApplication {
  public static void main(String[] args) {
    SpringApplication.run(DemoApplication.class, args);
  }

  @GetMapping("/")
  public String hello() {
    return "hello world!";
  }
}
 
 Once the application started, click on the Web Preview icon in the Cloud Shell toolbar and choose preview on port 8080.
 ./mvnw -DskipTests spring-boot:run
 gcloud app create --region us-central
 ./mvnw -DskipTests appengine:deploy
