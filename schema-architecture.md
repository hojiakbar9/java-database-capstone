# Section 1: Architecture Summary
This SpringBoot application follows a three-tier design architecture:
1. Presentation Tier—The user interface that consists of Thymeleaf templates and REST API consumers.
2. Application Tier—Backend that contains controllers, services, and business logic.
3. Data Tier—Databases: MySQL for structured data and MongoDB for flexible, document-based data.

For the Admin and Doctor dashboards Thymeleaf templates are used, whereas all other modules are served by REST APIs.
Both Thymeleaf and REST Controllers use the central Service layer that is responsible for retrieving the data from databases
and handles the application logic. MySQL uses JPA entities, while MongoDB uses document models.

#  Section 2: Flow of Data and Control
The interaction flow from the user interface to the data layer is detailed in the following seven steps:

1. User Initiation: A user initiates an action, either by navigating to an Admin/Doctor dashboard (triggering a Thymeleaf request) or by interacting with any other module (issuing a REST API call).

2. Request Interception: The incoming request is intercepted by the appropriate component in the Presentation Tier:
   - Thymeleaf Controllers handle dashboard requests (rendering views).
   - REST Controllers handle module requests (returning JSON data).

3. Service Layer Call: The Controller validates the request and delegates the responsibility to the central Service layer by calling the relevant business method.

4. Business Logic Execution: The Service layer executes the necessary business logic, validation, and authorization checks. It then determines which Data Tier resource is required (MySQL or MongoDB).

5. Data Access Layer Delegation: The Service layer calls the appropriate Repository/DAO (Data Access Object), utilizing JPA for MySQL entities or Spring Data MongoDB for document models, to perform the CRUD (Create, Read, Update, Delete) operation.

6. Response Generation (Success/Error): The Data Tier operation completes.
   - If successful, the Repository returns the requested data (or status) back to the Service layer.
   - If an error occurs (e.g., data not found, database error), an appropriate exception is thrown.

7. Final Response Delivery: The Service layer returns the processed result (data or error) back to the calling Controller, which then finalizes the response to the user:

   - Thymeleaf Controllers render the updated view.

   - REST Controllers package the response (as JSON) and return it to the client.