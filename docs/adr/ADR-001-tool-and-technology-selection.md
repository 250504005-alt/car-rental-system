# ADR-001: Tool and Technology Selection

- **Date:** 2026-11-23
- **Status:** Accepted
- **Participants:** Tugbanur, Yagmursu

## Context
To design the Car Rental System using a layered architecture and five design patterns (Strategy, State, Factory Method, Observer, Repository) and validate it with a working Java application, core development and documentation tools need to be selected[span_1](start_span)[span_1](end_span)[span_2](start_span)[span_2](end_span)[span_3](start_span)[span_3](end_span).

## Decision
- **Language:** Java 17+ — interfaces, abstract classes, and generics naturally express design patterns[span_4](start_span)[span_4](end_span).
- **IDE:** NetBeans — built-in Maven and JUnit support[span_5](start_span)[span_5](end_span).
- **Build Tool:** Maven — dependency management and standard project structure[span_6](start_span)[span_6](end_span).
- **Testing:** JUnit 5 — automated testing for pricing, booking conflicts, state transitions, and repository contracts[span_7](start_span)[span_7](end_span)[span_8](start_span)[span_8](end_span).
- **Database:** H2 (embedded) + JDBC — zero setup and easy transition from in-memory implementations via Repository interfaces[span_9](start_span)[span_9](end_span)[span_10](start_span)[span_10](end_span).
- **Diagrams:** PlantUML / draw.io — text-based sources support diff tracking in version control[span_11](start_span)[span_11](end_span).
- **Version Control:** Git + GitHub — branch protection, pull requests, and code review workflow[span_12](start_span)[span_12](end_span)[span_13](start_span)[span_13](end_span).

## Consequences
The team can collaborate in a buildable and testable Java/Maven environment while keeping out-of-scope items (real payment gateway integration, mobile/web UI, multi-branch support) excluded to preserve architectural focus[span_14](start_span)[span_14](end_span)[span_15](start_span)[span_15](end_span)[span_16](start_span)[span_16](end_span).
