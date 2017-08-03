# ConfigServerRepo
This repository contains external configurations for config clients

# Spring Boot AMC Starters 

Spring boot AMC starters is a spring framework code for AMC REST Service, where all the common REST libraries and auto configuration classes 
are bundled into as single easy to use spring boot starter artifact.

There are two flavours for the AMC spring boot starter. 
* Spring Boot AMC REST Starter

  Spring boot starter rest framework has a dependency to following spring modules
  
    * org.springframework.boot:spring-boot-starter-web, 
    * org.springframework.boot:spring-boot-starter-validation, 
    * io.springfox:springfox-swagger2:2.7.0, 
    * io.springfox:springfox-swagger-ui:2.7.0
    * com.github.lalyos:jfiglet:0.0.8,
    * org.springframework.boot:spring-boot-starter-test,
    * org.springframework:spring-test,
    * org.projectlombok:lombok
     
The Rest framework uses JFiglet dependency to draw ascii welcome banners dynamically using the name of the starter class. It configures swagger documentation 
plugin bean and auto configures docket api. 

* Spring Boot AMC MultiTenancy Starter. 

Multitenancy framework imports REST module and add its own set of dependencies associated to multitenant persistent framework. Multi tenancy framework
auto configures the project to use schema based multitenancy framework. The projects that bootstrap with multitenant framework will only need
to provide local and cloud databases configuration in their application.properties file and the framework will auto configure beans to read appropriate 
database properties based on the usage of @ActiveProfile annotation or active profile specified in the application.properties . 

  Spring boot starter multi tenancy framework has a dependency to following spring modules.
  
    * org.springframework.boot:spring-boot-starter-data-jpa,
    * net.bluemix:bluemix-cloud-connectors-cloudfoundry:0.0.1.RC6,
    * net.bluemix:bluemix-cloud-connectors-local:0.0.1.RC6,
    * commons-dbcp:1.4,
    * com.ibm.db2.jcc:db2jcc4:10.1

## Getting Started
You can checkout the the spring boot starters as gradle project locally and build the artifact using gradle.

``` 
./gradlew build
```

### Prerequisites
* Windows /Linux OS /Mac
* JDK 1.8
* Connected to Internet 


### Installing

* Checkout project to local folder.

```
git clone https://<user>@git.ng.bluemix.net/AMCBackend/spring-boot-amc-starters.git
git checkout develop
```

* Get into accounts project folder and execute gradle task
 
```
  ./gradlew build
```

This should take a while as it installs gradle, download project dependencies, build the project locally and run tests.
Once everything is built and tested you will have build folder created where you can find the project artifact.

AMC Starter rest boot starter
```
 <local folder>spring-boot-amc-starters\spring-boot-amc-starter-rest\build\libs\spring-boot-amc-starter-rest.jar
 ````
 AMC Starter multitenant boot starter
 ```
 <local folder>spring-boot-amc-starters\spring-boot-amc-starter-rest-multitenant\build\libs\spring-boot-amc-starter-rest-multitenant.jar
```


### Importing framework to  your REST service 
If you are using simple rest service than you can import the dependency in gradle like the following
```
compile 'com.accenture.amc:spring-boot-amc-starter-rest'
```
If you are using multitenant rest service than you can import the dependency in gradle like the following
```
compile 'com.accenture.amc:spring-boot-amc-starter-rest-multitenant'
```

Here is all the configuration you be necessary to successfully bootstrap the multi tenancy framework.

```
spring.jpa.database-platform=org.hibernate.dialect.DB2Dialect

jdbc:db2://dashdb-txn-small-yp-dal09-192.services.dal.bluemix.net:50000/BLUDB:retrieveMessagesFromServerOnGetMessage=true;
amc.database.url=jdbc:db2://dashdb-txn-small-yp-dal09-192.services.dal.bluemix.net:50000/BLUDB
amc.database.driver=com.ibm.db2.jcc.DB2Driver
amc.database.username=bluadmin
amc.database.password=YTg2OTA3NjM2M2Vj
```

 ## Running the tests

There are two test sample gradle module one testing the auto configuration of rest framework and other on multitenancy. 

* amc-spring-boot-multitenant-sample
* amc-spring-boot-restapp-sample
 

 ## Test Multitenancy 

 Once the build is done :

 Navigate to  amc-spring-boot-multitenant-sample:

 ```
cd amc-spring-boot-multitenant-sample

 ```

 Run the sample application : 
 ```
 ./gradlew bootRun

 ```

 Test the application by running the gradle test:

 ```
./gradlew test 

or 

./gradlew  test --tests com.accenture.amc.multitenant.config.CucumberRunner

 ```

## Deployment

Gradle deploy task will deploy the artifact to organisations nexus repository. ADOPS neuxs is a accenture's centrally managed
nexus repository and AMC release artifacts are deployed to this repository. 
Currently the rest framework release 1.2 is stable release for services wanting to use REST framework and 1.3 version of multitenant for projects
wanting to use multitenancy support.
Accounts Micro service is bootstraps 1.3 version of multitenant framework and is using DashDB has its multitenant database.

Example of deploying to nexus repository
```
gradlew uploadArchives
```

## Authors
* **Ganesh Raja** - *Initial work* 

## License
Accenture copy right.
