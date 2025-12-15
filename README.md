# provenance-data-pipeline

As part of my Fundamentals of Software Architecture for Big Data coursework, I was tasked with building a provenance app. A distributed RSS content aggregation system designed to ingest, process, and expose article metadata.

At a high level, the problem was simple: Reliably collect external content in the background with in-memory storage and expose it through a clean API. The real challenge was designing it as if it needed to scale, with clear boundaries, concurrency, and extensibility.

Here’s what I learned and why it matters:

- Module Architecture & Interface-Driven Design
  The system was split into independent modules (workflow, REST, RSS, domain logic), communicating through interfaces rather than implementations.
  This forces an implementation that let large systems grow, change, and scale with change-tolerant system design.

- Separation of Infrastructure from Business Logic
  Background scheduling, threading, and HTTP concerns were isolated from domain behavior.
  This pattern enables horizontal scaling, reuse across services, and easier migrations (like swapping in Spring Boot, a managed scheduler, or managed queue later).

- Workflow & Background Processing Patterns
  I implemented a configurable scheduler with concurrent execution using thread pools.
  The same design principles show up in ingestion pipelines, batch jobs, ETL systems, and async event consumers. A common problem I solve at Premier Roofing!

- Designing for Extensibility Over Premature Optimization
  Instead of hard-coding behaviors, the system exposed clear extension points for new workflows and data sources.
  This mindset is critical in large systems where requirements change faster than architectures.

This project reinforced key learnings in my growth as a software engineer. Scalability isn’t just about request per seconds. It’s also about structure, boundaries, and design decisions for rapid change.

Technologies Used (Determined by project requirements):

- Languages: Java and Kotlin
- Frameworks/Tools: Eclipse Jetty (embedded server), Jackson (JSON/XML parsing), Apache HTTP Components (HTTP client)
- Build/Deploy: Gradle multi-module project and Docker containerization
- Testing: JUnit and Mockito for unit/integration testing

Implementation Notes:

- I used in-memory storage to focus on architectural patterns as defined by the project requirements. Persistence using a database, thread-safety with a concurrent data structure, in-memory constraints, and query optimization are all further large scale design improvements that were not covered in this project.
- As per the course project requirements, I built the system using Eclipse Jetty to deeply understand HTTP request handling, routing, and lifecycle management. This can all be easily abstracted away with Spring Boot to improve the implementation for scale.
