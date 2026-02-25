# Laravel Backend Development Skill

A Claude Code skill for generating maintainable, idiomatic Laravel backend code.

## Overview

This skill activates when working with Laravel server-side features: controllers, models, migrations, API endpoints, services, jobs, events, policies, authentication, authorization, queues, and database operations.

## Key Conventions

- **Prefixed ULID IDs**: All models use string IDs with format `{prefix}_{ulid}` (e.g., `usr_01hzy3z4k8...`)
- **Versioned REST APIs**: All API routes must be versioned (`/api/v1/`, `/api/v2/`)
- **Artisan-first scaffolding**: Always use `php artisan make:*` commands
- **JsonResource responses**: API endpoints return resources, not raw models
- **Dependency injection**: No direct class instantiation; use DI or container resolution

## Code Quality Rules

- No nested `if` statements (use guard clauses)
- Prefer Laravel Collections over loops
- Thin controllers (validate, authorize, delegate, respond)
- Form Requests for validation; Policies for authorization
- Third-party services wrapped and registered in the container

## How to Trigger

This skill activates automatically when your prompt includes:

- **Keywords**: backend, API, endpoint, model, migration, controller, service, job, event, listener, policy, queue, authentication, authorization
- **Tasks**: Creating/modifying controllers, models, migrations, form requests, or any server-side PHP code
- **Features**: Building API endpoints, working with database schema, Eloquent relationships, or third-party integrations

**Examples:**
```
"Create a Post model with a comments relationship"
"Build a versioned API endpoint for user registration"
"Add a job to process image uploads"
"Set up authentication with Sanctum"
```

## Required MCPs

- **Context7**: Consult before implementing for latest Laravel patterns
- **Laravel AI SDK**: Required for all AI/LLM features (no direct provider SDKs)
- **Laravel Boost**: For scaffolding and convention alignment
- **Laravel Herd**: For local development and environment setup

## License

MIT
