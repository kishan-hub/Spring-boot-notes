# Spring-boot-notes
Spring Boot Short notes for Revision Any time


create The spring Boot Project using command line
mvn archetype:generate -DgroupId=boot -DartifactId=bootcore -Dversion=1.0.0 -DarchetypeGroupId=org.apache.maven.archetypes -DarchetypeArtifactId=maven-archetype-quickstart -DarchetypeVersion=1.4


Spring boot Stater depndency
----------------------------
<dependencies>
	<dependency>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter</artifactId>
		<version>2.7.3</version>
	</dependency>
</dependencies>

@SpringBootApplication
public class ClassName
{
   public static void main(String []args)
    {
      ApplicationContext context =SpringApplication.run(ClassName.class);

       Calander  cal = context.getBean(Calander.class);
         
       System.out.println(cal);
    }


}

@Component
public class Machine
{
    public void on(){}
}

@Configuration
@ComponenetScan(basePackage="com.coreioc.beans")
class JavaConfig
{
     @Bean  
     public Truck heavyTruck(){
     
         Truck truck=new Truck();
         truck.setModel("Ashoka truck");
         truck.capacity(5000);
      return truck;
     }
    
    @Bean
    public Truck mediumTruck(){
      Truck truck =new Truck();
       truck.setModel("Ashok truck");
        truck.setCapacity(5000);
     }

}


public class Test
{
    public static void main(String[]args)
    {
         ApplicationContext context=new AnnotationContextApplicationConfig(JavaConfig.class);
   
    }
}


@SpringBootApplication made it of combination of thread annotation
 1.@Configuration ->its self acts as configuration class
 2.@ComponentScan-> annoation is aplied with basepackages as the package.*
 3.@EnableAutoConfiguration = AutoConfiguration are not by default enabled, unless we write @EnableAutoConfiguration which will be added by default when we write @SpringBootApplication

Let us understand what will happens when we invoke SpringApplication.run(..) method:

The whole spring boot echo system has been wrapped into SpringApplication class, the static run method performs the below operations in running your spring boot application internally.

ApplicationContext context = SpringApplication.run(BootApplication.class, args);

1. creates an empty environment object
The Environment object of the ioc container is used for holding the configuration values, these values can be injected as depends into the Target classes for instantiating the objects for bean definitions
2. detects/identifies the external configuration of our application and gathers and loads the configuration into the Environment object created above
3. prints the spring boot banner
4. detects/identifies the type of the application by looking into the classpath of the project
	4.1 it checks under the classpath of the application, the spring mvc jar is found or not, if spring mvc jar is found, it treats the ApplicationType as WebApplication and creates the ioc container of type
	AnnotationConfigServletWebServerApplicationContext
	4.2 if Spring WebFlux dependecy is found under the classpath of the application, it treats the applicationType as REACTIVE and instantiates the ioc container of Type
	AnnotationConfigReactiveWebServerApplicationContext
	4.3 else it treats the WebApplicationType as None and instantiates the ioc container of type
	AnnotationConfigApplicationContext
5. It instantiates the spring factories (AutoConfiguration classes) and registers them with ioc container
6. Invokes the ApplicationContextInitializer
7. prepareContext()
8. refreshContext() = instantiates the objects for the bean definitions
9. executes the commandLineRunners and applicationRunners and returns the reference of the ioc container to us
10. during the above stages of operations, the SpringApplication class publishes different events and triggers the Listener classes for handling the events





//create the Jar file using comandPromt

Let us try to understand typical java application
---------------------------------------------------
travelgo
 |-src
    |->travelgo
          |-service
               |->TravelGoservice.java

 |->bin
     |->com
         |->travelgo
             |->service
                  |->TravelGoService.class
compile the java program

javac -d bin src\com\travelgo\service\TravelGoService.java 

Execute the java Program
---------------------------
1.set the class path
set classpath=c:\Users\KISHANTECH\spring-boot-workspace\travelgo\bin

2.java com.travelgo.service.TravelGoService


create the jar file
--------------------
jar -cvf travelgo.jar bin\* 

Execute the application using jar file
---------------------------------------
1.set the classpath

   set classpath=c:\Users\KISHANTECH\spring-boot-workspace\travelgo\bin\travelgo.jar

2. execute the jar file
 

