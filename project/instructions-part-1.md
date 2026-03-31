# Airport Management System — Part 1: Architecture Design

---

### Change log

- 31-03-2026: Added a clarification in the "Working Teams" section, regarding team splitting and joining in later
  parts of the project.

## Introduction

This document describes Part 1 of the Airport Management System project for the course **Internet Applications Design
and Implementation**. In this part, you are required to **design** the system — no implementation code is expected yet.

For Part 1, your task is to:

- Partition the domain into several independent microservices using the __database per service__ pattern
- For each microservice, produce two design artefacts:
    - An **Entity-Relationship (E/R) diagram** capturing the data model.
        - Virtual FKs should be clearly marked as such.
    - A **REST API specification** covering all resources and operations exposed by the service.

For Parts 2 and 3, you will implement only a subset of the overall system. If there are significant differences between
the architectures defined in Part 1 and those used in Part 2, you must provide a clear justification. Design your
solutions carefully to avoid unnecessary deviations.

## Domain description

The system manages all information related to the commercial air transport operations of the airport. It also manages
the people who travel through the airport and the commercial bookings that link them to flights. A passenger is a person
registered in the system with a unique email address. Each passenger may hold multiple travel documents (such as
passports or national identity cards), each of a different type or from a different issuing country.

A booking represents a reservation for one or more passengers on a specific flight. Group bookings — where multiple
passengers share a single booking reference — are supported; equally, a single passenger may have many bookings over
time. Each booking contains one or more tickets; each ticket corresponds to one passenger within the booking and records
the assigned seat, travel class, and price paid. Passengers must be able to register and manage their profile and travel
documents, and create and manage their bookings. Check-in Agents must be able to look up passengers and bookings, assign
seats by creating tickets, and update booking statuses. Airport Administrators must be able to manage any passenger
record or booking. When a passenger checks in, a baggage claim is opened referencing the passenger, the booking, and the
flight. Individual items are registered under the claim, each identified by a unique tag number. A formal receipt can be
issued once all items are registered. As items move through the airport they pass through handling zones (screening
belts, sorting carousels, loading bays, etc.), each associated with a terminal by its identifier; each transit is
recorded. An item passes through many zones and a zone processes many items. Unclaimed or missing items can be logged in
a lost-and-found register and later matched to a baggage item. Check-in Agents must be able to open claims, register
baggage items, and issue receipts. Baggage Handlers must be able to record transit events through handling zones and
link lost-and-found reports to matched items. Airport Administrators must be able to manage handling zones and
lost-and-found reports. Passengers must be able to report missing items.

Each flight belongs to exactly one airline and carries a flight number that is unique within that airline. Airlines are
identified by a globally unique IATA code. Every flight is governed by exactly one
schedule, which captures the planned departure and arrival times, days of operation, and other operational parameters. A
flight may have zero or more intermediate stops, each representing a point along the route between origin and
destination; stops are ordered and their sequence matters. The service also maintains a shared catalogue of in-flight
amenities (such as meal service, Wi-Fi, or entertainment). A given amenity can be offered on many flights, and a flight
can offer many amenities. The system must allow passengers to search for flights by route (origin and/or destination),
airline, status, and date of operation so that it can find flights relevant to their travel plans. Airline
representatives must be able to register and manage their airline, declare the aircraft types in their fleet, and create
and manage flights, including schedules, intermediate stops, and amenity assignments.
Airport Administrators must be able to manage the global amenity catalogue and update the operational status of any
flight.

The system tracks the end-to-end travel experience of each passenger through a Journey resource, which aggregates
information from bookings, baggage, and flight operations into a single view of the passenger's current state. A journey
is opened when a passenger confirms a booking and progresses through a sequence of phases: once the booking is confirmed
the journey starts as `BOOKED`; when the passenger checks in and a seat is assigned the journey advances to
`CHECKED_IN`; dropping off baggage and registering all items under a claim moves the journey to `BAGGAGE_DROPPED`;
flight departure advances it to `IN_FLIGHT`; landing sets the journey to `ARRIVED`; and once the passenger collects
their baggage the journey reaches `COMPLETED`. Passengers must be able to view their current journey state and their
journey
history.

## Working Teams

The project assignment should be done by teams of 2 or 3. If you cannot make a team of 2 or 3, talk to the instructor to
authorize other solutions.

To register your team, you will receive a GitHub Classroom invite link — check your email or CLIP Messages.
When creating your team, use your student numbers as the team name, ordered from lowest to highest and separated them
by `_` (e.g., `70001_70002_70003`). Once the team is created, the remaining members can join it and access the team's
repository.

Teams must remain the same for Parts 2 and 3 of the project. In exceptional and justified situations, a student may
leave their team and continue the project individually, but only after discussing it with the instructor and receiving
approval. Under no circumstances may a student join a different team in later parts.

## Assignment Submission

This assignment must be completed and submitted via GitHub. Push your final version of Part 1 to your team's repository
before the deadline. Only the last commit before the deadline will be considered; late submissions will not
be accepted. Please ensure your repository is correctly structured and includes all required files. If you experience
any issues with GitHub Classroom, contact us as soon as possible.

## Deliverables

Submit an ARCHITECTURE.md file in the root of the repository with a general description of the system architecture
followed by a list of the microservices and their respective design artefacts. It should also include the number and
name of the students in the team.

The E/R diagrams must clearly show the relationships between the entities (including cardinality) and their attributes.
The diagrams must be embedded in the ARCHITECTURE.md file and reference local files.

The REST API specification doesn't need to be an OpenAPI specification. At this point, a table like this will suffice:

### Service XYZ

| Method | Path       | Description           |
|--------|------------|-----------------------|
| GET    | `/bananas` | Get a list of bananas |

No need to describe the JSON structure of the requests and responses. However, if the endpoint accepts query parameters,
they should be listed in the table.

Include a section at the end of the document that justifies the design choices made.

## Grading

This part is ungraded but mandatory. To be considered for evaluation, your repository must include an
ARCHITECTURE.md file in its root directory. This file should list all microservices and include their corresponding
design artifacts.

## Deadline

This part is due on **6 April 2026 (until 23h59)**.