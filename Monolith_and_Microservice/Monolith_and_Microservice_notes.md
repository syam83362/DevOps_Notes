# What is Monolithic Architecture?

A **monolithic architecture** is an application architecture where multiple services or features are developed and deployed as a **single application**.

For example, consider an application like Paytm. It may provide multiple services such as:

- Money transactions
- Movie tickets
- Train tickets
- Bus tickets
- Other services

In a monolithic architecture, all these services are part of the **same application** and are deployed together.

### Scenario

Suppose there is a bug in the movie-ticket service.

If we need to stop the application to fix and deploy the change, the **entire application may become unavailable** during that time.

This is one of the disadvantages of monolithic architecture.

Because of such limitations, applications can be designed using **microservices architecture**.

# What are Microservices?

**Microservices architecture** is an approach where an application is divided into multiple smaller, independent services.

For example, a Paytm-like application can have separate services for:

- Money transactions
- Movie tickets
- Train tickets
- Bus tickets
- Other services

Each service can be developed, deployed, and managed independently.

This means that if one service has a problem, we can work on that service without necessarily stopping the entire application.

Each microservice can also have its **own database**, depending on the application's design.

### Simple Difference

**Monolithic:**

`Application → All services together`

**Microservices:**

`Application → Service 1 | Service 2 | Service 3 | ...`
