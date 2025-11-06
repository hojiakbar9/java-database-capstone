# Architecture Summary
This SpringBoot application follows a three-tier design architecture:
1. Presentation Tier—The user interface that consists of Thymeleaf templates and REST API consumers.
2. Application Tier—Backend that contains controllers, services, and business logic.
3. Data Tier—Databases: MySQL for structured data and MongoDB for flexible, document-based data.

For the Admin and Doctor dashboards Thymeleaf templates are used, whereas all other modules are served by REST APIs.
Both Thymeleaf and REST Controllers use the central Service layer that is responsible for retrieving the data from databases
and handles the application logic. MySQL uses JPA entities, while MongoDB uses document models.

# Flow of Data and Control
1. User accesses one of the available dashboards or REST Modules.
2. The action is intercepted by the appropriate Thymeleaf or REST Controller.
3. The (Thymeleaf or REST) controller calls the Service layer.
4. The Service layer delegates the appropriate database and returns the requested data if successful or throws an error if not.