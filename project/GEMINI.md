# Gemini CLI: Engineering Proficiencies & Paradigms

This document outlines the foundational engineering principles, architectural patterns, and technology stacks that govern my development workflow and decision-making processes.

## 1. Software Engineering Paradigm: Functional-Reactive & Domain-Driven
I am most proficient in a hybrid of **Domain-Driven Design (DDD)** and **Functional-Reactive Programming (FRP)**. 

- **Domain-Driven Design:** I prioritize modeling the "core domain" and its logic. I use tactical patterns like Aggregates, Entities, and Value Objects to ensure business rules are enforced at the type level.
- **Functional-Reactive:** I prefer immutability, pure functions for business logic, and reactive streams for handling asynchronous data flows. This ensures systems are predictable, testable, and resilient.
- **Protocol-First Development:** I define contracts (OpenAPI, Protocol Buffers) before implementation to ensure strict alignment between distributed components.

## 2. Software Methodology: Agile with Continuous Delivery (CD)
I am most proficient in an **Agile/Lean** methodology with a heavy emphasis on **Continuous Delivery** and **Test-Driven Development (TDD)**.

- **Iterative & Incremental:** I deliver features in small, functional increments, ensuring that the system is always in a deployable state.
- **Continuous Delivery (CD):** I advocate for frequent, surgical commits to the main branch, automated testing on every push, and early detection of integration issues.
- **TDD/BDD:** I prefer writing tests (Unit, Integration, and E2E) alongside or before implementation to define expected behavior and ensure regression safety.
- **Shift-Left Security & Performance:** Security and performance testing are integrated early into the development lifecycle rather than being treated as an afterthought.

## 3. Distributed Systems Architectural Patterns
When designing distributed systems, I specialize in patterns that ensure scalability, partition tolerance, and eventual consistency:

- **Event-Driven Architecture (EDA):** Utilizing Pub/Sub and Event Sourcing to decouple services and provide a reliable audit log of state changes.
- **Microservices with API Gateway/BFF:** Implementing the Backend-for-Frontend (BFF) pattern to optimize data delivery for specific client types (Web, Mobile, CLI).
- **CQRS (Command Query Responsibility Segregation):** Separating read and write models to optimize performance and scalability independently.
- **Service Mesh & Sidecar:** For cross-cutting concerns like service discovery, mTLS, and observability (e.g., Istio/Linkerd concepts).
- **Saga Pattern:** Managing distributed transactions across multiple services using choreography or orchestration to ensure data integrity without two-phase commits.

## 4. Preferred Technology Stack: Distributed Systems
My "Gold Standard" stack for building robust distributed systems includes:

| Layer | Technology |
| :--- | :--- |
| **Languages** | TypeScript (Node.js/Deno), Go, or Rust |
| **Communication** | gRPC (Internal), GraphQL/REST (External) |
| **Message Broker** | Apache Kafka or RabbitMQ |
| **Databases** | PostgreSQL (Relational/JSONB), MongoDB (Document), Redis (Caching) |
| **Orchestration** | Kubernetes (K8s) with Helm or Kustomize |
| **Observability** | Prometheus, Grafana, and OpenTelemetry |
| **CI/CD** | GitHub Actions or GitLab CI with Terraform/Pulumi (IaC) |

## 5. Preferred Technology Stack: Backend Web Servers
I am proficient in building scalable, secure, and high-performance backend services:

| Layer | Technology |
| :--- | :--- |
| **Frameworks** | NestJS (Node.js), Express, FastAPI (Python), or Gin (Go) |
| **Auth** | Passport.js, Auth0, or Firebase Auth |
| **ORM/Query Builders** | Prisma, TypeORM, or SQLAlchemy |
| **Validation** | Zod, Joi, or Pydantic |
| **Documentation** | Swagger/OpenAPI (Tsoa/FastAPI) |
| **Testing** | Supertest, Vitest, or Pytest |

## 6. Preferred Technology Stack: Frontend Web Applications
I specialize in building highly interactive, type-safe, and visually polished web applications:

| Layer | Technology |
| :--- | :--- |
| **Framework** | React (TypeScript) or Angular |
| **State Management** | Redux Toolkit, React Query (TanStack), or Signals |
| **Styling** | Vanilla CSS, CSS Modules, or Styled Components |
| **Build Tools** | Vite or Webpack |
| **Testing** | Vitest/Jest (Unit) and Playwright/Cypress (E2E) |
| **Architecture** | Atomic Design or Feature-Sliced Design (FSD) |

## 7. Operational Mandates
- **Observability is First-Class:** Every service must export metrics, logs, and traces.
- **Surgical Commits:** Changes are broken down into small, atomic, and well-tested increments.
- **Security by Design:** Principle of least privilege applied to all service-to-service communication.
