# Airport Management System — Part 2: Backend Implementation

---

## Introduction

In Part 2, your team must implement a **working subset** of the Airport Management System designed in Part 1.

The implementation must follow a **microservices architecture** using:

- Database per service pattern
- API Gateway
- Service Discovery
- MySQL databases

You are **not required to implement the full system** from Part 1. Instead, you must implement the **minimum set of
modules, endpoints, and data structures** necessary to support:

- all **mandatory user stories**
- **two additional user stories** defined by your team

Your implementation must remain **consistent with the architecture defined in Part 1**. Any relevant changes must be
explicitly documented and justified.

## General Requirements

### Architecture

The project must be implemented as a **multi-module Maven project** including:

- one module per microservice
- one module for Service Discovery
- one module for the API Gateway
- one module for the web application

All communication must respect microservices architecture principles taught in class.

### Technology Stack

You must use:

- Spring Boot 3.5.x
- Kotlin
- MySQL
- Maven (multi-module)

Any deviation must be justified.

## API and Documentation

### OpenAPI

Each microservice must expose and document its API using **OpenAPI**.

Only implemented endpoints need to be documented.

### API Gateway

All endpoints must be accessible **through the API Gateway**, which must:

- route requests to services
- validate API tokens (all requests must include an `X-Api-Key` header)
- enforce authentication when required

Note: In Part 2, you will not implement any direct client of the API Gateway. Therefore, the API Gateway must be tested
using the IntelliJ HTTP Client (HTTP Requests feature). You must provide an `api.http` file containing example requests
for **all endpoints exposed through the API Gateway**, including any required headers (e.g., `X-Api-Token`,
authentication tokens).

## Web Application

You must implement an **independent SSR web application** that:

- supports both **staff (backoffice)** and **passengers (frontoffice)**
- is a multi-page application
- includes a navigation bar
- follows a RESTful approach for the endpoints using the _method overriding_ technique
- does not include any custom JavaScript but may use third-party libraries such as Bootstrap or HTMX.
- may have its own database if justified

## Authentication

All services must use **JWT authentication**

### Web Application

All operations must be authenticated, with no server-side sessions, using JWT stored in the browser.

#### Option 1

- All users log in via form

#### Option 2 (more complex, higher value)

- Staff: login form
- Passengers: OAuth2 (e.g., GitHub)

### Initial Users

- At least **2 users per role**

If using OAuth2:

- staff users must be pre-created
- passengers must NOT be pre-created

## Authorization

You should use the RBAC and MBAC techniques taught in the classes and follow the best practices to implement them.

## Testing

All microservices and the web application must include automated unit and integration tests (coverage must be at least
50% per module).

## Initial Data

All implemented list endpoints must return **at least 3 items**.

## User Stories

You must implement the following user stories:

- As an Airline Representative, I want to create flights so that they can be booked by passengers.
- As a Passenger, I want to search for flights by origin, destination, and travel date so that I can plan my trip.
- As a Passenger, I want to create a booking for a flight so that I can reserve my travel.
- As a Passenger, I want to include multiple passengers in a booking so that I can travel in a group.
- As a Passenger, I want to access bookings I am associated with so that I can view my travel details (even if I am not
  the creator).
- As a Passenger, I want to cancel a booking I created.
- As a Check-in Agent, I want to look up passengers so that I can assist them.
- As a Check-in Agent, I want to look up bookings so that I can manage check-in operations.
- As a Check-in Agent, I want to check in passengers with existing bookings by assigning them seats and issuing tickets
  so that they are ready to board their flight.
- As an Airport Administrator, I want to update a flight’s operational status (e.g., scheduled, in-flight, arrived) so
  that its real-time progress is accurately tracked.
- As a Passenger, I want to view my journeys so that I can track my travel progress.
- As a Passenger, I want to view the details of my current journey so that I know my current status.

Additionally, you must define and implement **2 additional user stories**, documented in `ADDITIONAL_USER_STORIES.md`.
User stories with higher complexity (e.g., involving multiple microservices or complex data relationships) will be
valued more highly in the evaluation.

## Team Rules

- Teams must remain the same as Part 1
- Work must be distributed across members
- Responsibilities must be documented
- Each member must have **at least 5 non-trivial commits**

## Deliverables

### 1. Updated `ARCHITECTURE.md`

Must include:

- implemented microservices
- implemented endpoints
- RBAC and MBAC rules
- security section
- database changes
- changelog from Part 1

### 2. `ADDITIONAL_USER_STORIES.md`

Must describe the two additional user stories.

### 3. OpenAPI Documentation - several `API_<MICROSERVICE_NAME>.pdf`

- one per microservice
- exported as PDF

### 4. `TEST_REPORT.md`

- test results
- coverage report

### 5. Maven Project

The project must be implemented as a single multi-module maven project in the root of the repository

- microservices modules
- service discovery module
- API gateway module
- web application module

### 6. `docker-compose.yml`

A single docker-compose file in the root of the repository that starts all MySQL instances required by the different
modules, each configured with its own dedicated application user.

### 7. `api.http`

Must include example requests for all endpoints provided by the API Gateway.

### 8. `README.md`

Must include:

- team members and contributions (be explicit about who did what)
- run and test instructions
- pre-created users (username/password/role)
- link to a video presenting the interactions with the microservices using the previous api.http file (max. 2 minutes)
- link to a video presenting the interaction with the backoffice showing all the user stories (max. 4 minutes)
- self-assessment table (see below)
- conclusions: learning outcomes, challenges, difficulties, time spent, positive aspects, not positive aspects of the
  project.

#### Video Rules

- must be published on YouTube as unlisted videos
- must include narration (Portuguese or English)

#### Self-assessment

Present a table with the self-assessment using percentages of fulfillment in the following topics (100% it’s perfect, >
50% needs improvement, <50% has flaws or is incomplete):

* Architecture Consistency with Part 1
* Microservices Design Quality
* API Design & RESTfulness (as documented by OpenAPI)
* API Gateway & Service Discovery
* Authentication Implementation
* Authorization (RBAC & MBAC)
* Web Application Quality (SSR, usability, correct interaction with services)
* User Stories Coverage (completeness and correctness of implemented stories)
* Data Modeling & Persistence
* Testing Quality (unit and integration tests, coverage, relevance)
* Logging & Observability
* Code Quality & Organization
* Complexity of Additional User Stories
* DevOps & Setup (docker-compose, ease of running the system)
* Demonstration videos

---

## Submission

The project must be submitted using the same GitHub repository created in Part 1.

## Use of AI tools

The use of AI tools is allowed and encouraged, provided you fully understand all generated code; regardless of its
origin, you are responsible for ensuring it works correctly and adheres to best practices.

There will be a project discussion after Part 3 in which each team member will be required to modify the project’s code
to meet new requirements without AI assistance; failure to do so may result in penalties or even failing the project.

## Deadline

**6 May 2026 — 23:59**