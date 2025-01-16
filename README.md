# Credit Score Analysis Tool Prototype Code Explanation

**Important Note:** This project may or may not work. The idea behind writing and sharing the code with you is to help you understand how different parts of the project connect and work together. It’s a small prototype codebase. For example, we have used Log4j2 in one method only to demonstrate its functionality, but in an enterprise project, we would use every service/tool throughout the project. Additionally, real enterprise projects contain hundreds of thousands of lines of code, and it’s nearly impossible to create an exact enterprise project.

## 1. Project Overview
We have created three microservices here: **CreditScoringService**, **UserManagement**, and **SpringCloudGateway** (UI is directly connecting to this service and further this service is rerouting the requests to the different microservices).

**Note:** In enterprise projects, there may be a lot of microservices. Since this is a prototype-based project, we have just created three to demonstrate how things work.

### The details for each microservice:
- Inside our projects, we have **src/main/java** that contains the main code of our application.
- **src/main/resources** contains the **application.properties** file for setting the properties of different tools such as Kafka, Redis, etc.
- **src/test/java** contains test classes and test cases for Sonar coverage as well as for testing the entire application.
- In the end, we have **pom.xml** that contains dependencies to make it a complete Spring Boot application.

Our main focus will be on **src/main/java** for each service.

### Main packages:
- **Main Package**: This is the main package where the application's entry point, usually the **main()** method, is defined. This method is responsible for booting the application.
- **Config Package**: In this package, all the configuration and setup are done for different tools and services.
- **Controller Package**: This package contains the REST API controllers. Controllers handle incoming HTTP requests and respond with the appropriate HTTP responses. They act as the interface between the frontend and the backend services.
- **DTO (Data Transfer Objects) Package**: DTOs are simple objects used to transfer data between processes, primarily between your controllers and services. They do not contain any business logic.
- **Entity Package**: This package includes the entity classes, which map to the database tables through ORM (Object Relational Mapping). These classes typically contain Hibernate or JPA annotations that describe the database table structure.
- **Filter Package**: This package contains filters used in the web layer, such as logging, authentication, or preprocessing requests before they reach the controllers.
- **Repository Package**: This package contains interfaces that extend **JpaRepository** or similar Spring Data interfaces. Repositories abstract the data layer, providing an elegant way to perform CRUD operations on the database.
- **Service Package**: Services contain the business logic of the application. They interact with repositories to fetch and store data, perform calculations, and handle business rules.

**Note:** We haven’t implemented everything in every microservice. In **CreditScoringServiceMS**, we have implemented Redis Cache, Kafka, Email, Log4j2, and Splunk. In **UserManagementMS**, we have implemented login and registration with OAuth. In one scenario, we are consuming one **UserManagementMS** API by **CreditScoringServiceMS**. **SpringCloudGateway MS** is just for routing the APIs from UI to different microservices.

## 2. How Redis Cache is integrated in CreditScoringServiceMS:
We added Redis dependencies in the **pom.xml** file to integrate Redis Cache into **CreditScoringServiceMS**.

## Microservices:
The application is split into microservices that can be set up independently. Each service handles a different part of the application, making it simpler to manage, easier to fix and update, and allows for easier scalability.

### Microservices in this project:
- **Data Collection Service**: It manages the ingestion and preprocessing of financial data from various sources.
- **Credit Scoring Service**: It handles the calculation of credit scores using a predefined algorithm. This service processes input from the **Data Collection Service**.
- **User Management Service**: This service manages user login and registration through OAuth and integrates with the other services as required.
- **Spring Cloud Gateway**: It acts as the single-entry point for all client requests to the backend services. It routes requests to the appropriate microservices and provides common functionalities like authentication and logging. Spring Cloud Gateway is used to route and filter traffic to microservices, simplifying and securing communication between the services.

## 3. Application Structure:
This project utilizes a microservice architecture with services such as credit scoring, user management, and API gateway to ensure scalability and efficient handling of different service components. Each microservice operates independently and provides a specific set of functions that contribute to the overall credit score analysis tool.
