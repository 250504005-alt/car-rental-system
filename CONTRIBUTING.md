# Contributing Guide

Shared working conventions for the `car-rental-system` repository[span_17](start_span)[span_17](end_span)[span_18](start_span)[span_18](end_span):

## Git and Pull Request Workflow
- The `main` branch must always remain in a working state; direct pushes are not allowed[span_19](start_span)[span_19](end_span)[span_20](start_span)[span_20](end_span).
- All work is done in separate branches (`feature/...`, `docs/...`, `test/...`) and merged into `main` via Pull Requests (PR)[span_21](start_span)[span_21](end_span)[span_22](start_span)[span_22](end_span).
- Every PR is reviewed by the other team member before merging[span_23](start_span)[span_23](end_span).
- During implementation, every PR must include at least one test[span_24](start_span)[span_24](end_span).

## Commit Message Format
- `feat:` new feature or class
- `docs:` documentation, ADR, or diagram
- `test:` unit or integration test
- `fix:` bug fix
- `refactor:` structural refactoring

## Naming and Coding Standards
- Classes / Interfaces / Enums: `PascalCase`
- Methods / Variables: `camelCase`
- Constants: `UPPER_SNAKE_CASE`
- Packages: lowercase (`com.carrental.*`)[span_25](start_span)[span_25](end_span)
- Service classes depend on interfaces, with dependencies provided via constructor injection[span_26](start_span)[span_26](end_span).
- Business rules reside in Service/Domain layers rather than the UI layer[span_27](start_span)[span_27](end_span).
- All `public` classes and methods have Javadoc comments[span_28](start_span)[span_28](end_span).
