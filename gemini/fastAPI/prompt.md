You are the senior backend architect and engineer for this project.

Read and follow the `GEMINI.md` file in the repository root as the source of engineering and architectural guidelines.

Your first task is **NOT to modify the code**.

I want you to deeply analyze the existing repository and determine how we should evolve it into a production-grade FastAPI backend following the principles defined in `GEMINI.md`.

## Phase 1 — Repository Understanding

Inspect the repository and understand:

- Current project structure
- Existing FastAPI implementation
- Existing API routes
- Services and business logic
- Database access
- MongoDB usage
- Models and schemas
- Authentication/authorization
- Configuration
- Logging
- Error handling
- External integrations
- Bitbucket usage
- Existing storage abstractions
- WebSocket implementation, if any
- Singleton-style components/APIs
- Background jobs/tasks
- Tests
- Docker/deployment configuration
- Dependency management

Do not make changes during this phase.

## Phase 2 — Architecture Gap Analysis

Compare the current implementation against `GEMINI.md`.

Identify:

1. What is already implemented correctly
2. What partially exists
3. What is missing
4. What should be refactored
5. What should NOT be changed because the current implementation is already appropriate
6. Architectural risks
7. Scalability risks
8. Security risks
9. Technical debt
10. Potential future migration problems

Pay particular attention to these architectural requirements:

### Database

MongoDB is the current database, but the architecture should allow another database in the future without rewriting business logic.

### Storage

Bitbucket is currently being used for storage.

GCS will be introduced and Bitbucket will eventually be migrated away from.

The application should therefore have a clean storage abstraction so business logic does not depend directly on Bitbucket or GCS.

### Third-party integrations

The system will eventually integrate with multiple external/third-party services.

Identify where an integration/adapter architecture would be useful.

### Singleton systems

Identify APIs/components that require singleton behavior.

Determine whether each singleton requirement is:

- Process-level
- Application-level
- Worker-level
- Distributed

Do not assume an in-memory singleton is sufficient for a horizontally scaled application.

### WebSockets

Determine the current WebSocket architecture, if any.

Evaluate:

- Connection management
- Authentication
- Broadcasting
- Error handling
- Lifecycle management
- Multi-instance scalability
- Whether a message broker will eventually be required

Do not introduce Redis or another broker unless the current architecture actually requires it.

## Phase 3 — Produce an Architecture Report

Do not modify any files yet.

Give me a concise but technically useful report.

Start with:

### Current Architecture

Explain the current architecture in simple terms.

Then provide:

### Architecture Gap Analysis

Use this table:

| Area | Current State | Target State | Gap | Priority |
|------|---------------|--------------|-----|----------|
| API | | | | |
| Database | | | | |
| Storage | | | | |
| Services | | | | |
| Third-party integrations | | | | |
| Singleton systems | | | | |
| WebSockets | | | | |
| Authentication | | | | |
| Configuration | | | | |
| Logging | | | | |
| Testing | | | | |
| Deployment | | | | |

Then provide:

### Recommended Project Structure

Show the proposed folder structure, but only include directories that are actually justified by the repository.

### Required Changes

Create a prioritized list:

```text
P0 — Required architectural changes
P1 — Important improvements
P2 — Future improvements
```

For every change, mention:

- File(s) affected
- What needs to change
- Why
- Risk
- Dependencies

### Migration Strategy

Explain how we can move from:

Bitbucket → GCS

without breaking existing functionality.

Include a phased approach if appropriate.

### WebSocket Strategy

Explain how WebSockets should work now and what would need to change when the backend runs across multiple instances.

### Database Strategy

Explain how MongoDB should be isolated so another database can be introduced later without unnecessarily over-engineering the current implementation.

### Final Recommendation

End with:

1. What should be changed immediately
2. What should be left untouched
3. What should be designed for future migration
4. What should NOT be introduced yet
5. Recommended implementation order

## Important Constraints

- Do NOT modify files.
- Do NOT create files.
- Do NOT install dependencies.
- Do NOT rewrite the existing architecture just because `GEMINI.md` recommends a pattern.
- Prefer existing project conventions when they are good.
- Do not introduce unnecessary abstractions.
- Do not introduce technologies such as Redis, Kafka, Celery, PostgreSQL, etc. without a concrete architectural reason.
- Identify existing code before proposing new code.
- Do not assume requirements that are not present in the repository.
- Be especially careful about backward compatibility.
- Keep the analysis concise enough that it can be reviewed by a senior engineer.

At the end, provide a clear section:

## Recommended Implementation Plan

Give me the implementation plan in small, independently reviewable steps.

I will review the plan before asking you to make any changes.
