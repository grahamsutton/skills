---
name: backend-development
description: "Generates maintainable, idiomatic Laravel backend code. Activates when creating controllers, models, migrations, API endpoints, services, jobs, events, policies, form requests, or any server-side PHP code; when working with database schema, Eloquent relationships, authentication, authorization, queues, or third-party integrations; when the user mentions backend, API, endpoint, model, migration, controller, service, job, or any Laravel server-side feature. This skill should be active for nearly all code generation tasks."
license: MIT
metadata:
  author: Graham Sutton
---

# Backend Development

## When to Apply

Activate this skill when:

- Creating or modifying controllers, models, migrations, or any backend PHP code
- Building API endpoints (versioned REST APIs)
- Working with database schema, relationships, or queries
- Implementing services, jobs, events, listeners, or policies
- Setting up authentication, authorization, or third-party integrations
- Any server-side Laravel development task

## Purpose

Generate maintainable, readable, idiomatic Laravel backend code.

Priorities:

- Architectural integrity
- Clarity over cleverness
- Strict REST discipline
- Deterministic ID strategy
- Secure-by-default behavior
- Long-term maintainability

All implementations must follow modern Laravel best practices and current ecosystem standards.

---

## Mandatory MCP Usage

### 1) Context7 MCP (REQUIRED)

- ALWAYS consult Context7 before implementing.
- Ensure usage of the latest stable Laravel APIs and ecosystem patterns.
- Avoid deprecated approaches.
- Prefer modern idiomatic Laravel solutions.

### 2) Laravel AI SDK (REQUIRED for AI/LLM features)

- ALL AI/LLM interactions MUST use `laravel/ai`.
- NEVER directly call OpenAI, Anthropic, or other provider SDKs.
- Use Laravel AI abstractions and config-driven providers.
- Official documentation (always consult, since this package is new):
  https://laravel.com/docs/12.x/ai-sdk.md
- ALWAYS verify usage via Context7 + the official docs above before implementing.

### 3) Laravel Boost MCP

- Use Laravel Boost MCP when scaffolding features, refactoring code, or aligning with Laravel conventions.
- Prefer Boost-supported scaffolding patterns when applicable.

### 4) Laravel Herd MCP

- Use Laravel Herd MCP when environment setup, local development workflows, services, or runtime configurations are relevant.
- Ensure local-first development compatibility.

---

## Artisan Command Requirements (MANDATORY)

When creating files, ALWAYS use Laravel Artisan commands so files are created in correct locations:

Examples:

- Controllers: `php artisan make:controller`
- Models: `php artisan make:model`
- Migrations: `php artisan make:migration`
- Form Requests: `php artisan make:request`
- Policies: `php artisan make:policy`
- Jobs: `php artisan make:job`
- Events: `php artisan make:event`
- Listeners: `php artisan make:listener`
- Tests: `php artisan make:test`
- AI agents: use artisan commands provided by `laravel/ai`

Do NOT manually create files when an Artisan generator exists.

### Exception: Enums

- DO NOT use `php artisan make:enum`.
- Enums must be created manually in `app/Enums`.
- Must follow PSR-4 namespace conventions and be explicitly typed and readable.

---

## Mandatory Model ID Strategy (CRITICAL)

### ID Format

All models MUST use string IDs with the format:

`{three_letter_prefix}_{lowercase_ulid}`

Example:
`usr_01hzy3z4k8y7abcde123456789`

### Model Requirements

- Every Eloquent model MUST:
  - Use `App\Models\Concerns\HasPrefixedUlid`
  - Define `protected static string $ulidPrefix = 'abc';` (exactly 3 lowercase letters)
- No model may use integer IDs.
- No part of the codebase may assume integer IDs.

### Migration Requirements

- NEVER use:
  - `$table->id()`
  - `$table->foreignId()`
  - `$table->ulid()`
- ALWAYS use:
  - `$table->string('id')->primary();`

### Foreign Key Requirements (string-based)

- Foreign keys must be declared as strings:
  - `$table->string('user_id');`
- Foreign key constraints must be explicit:
  - `$table->foreign('user_id')->references('id')->on('users')->cascadeOnDelete();`

### Framework Default Migrations

All default migrations shipped with Laravel MUST be adjusted to support string primary keys and string foreign keys (replace `$table->id()` and `$table->foreignId()` patterns everywhere).

---

## Foundational Trait Requirement: HasPrefixedUlid (Canonical)

This trait is foundational and authoritative.

- The agent MUST NOT modify or reimplement this trait unless explicitly instructed.
- If the trait does not exist, the agent MUST create it EXACTLY as specified below.
- STRICT POLICY A is required: if a model does not define a valid `$ulidPrefix`, the trait MUST throw.

**File path:**
`app/Models/Concerns/HasPrefixedUlid.php`

**Canonical implementation (DO NOT CHANGE):**

```php
<?php

namespace App\Models\Concerns;

use Illuminate\Support\Str;
use RuntimeException;

trait HasPrefixedUlid
{
    /**
     * Models MUST override this with a 3-letter lowercase prefix.
     *
     * Example:
     *   protected static string $ulidPrefix = 'usr';
     */
    protected static ?string $ulidPrefix = null;

    /**
     * Boot the trait.
     */
    protected static function bootHasPrefixedUlid(): void
    {
        static::creating(function ($model) {
            if (!$model->getKey()) {
                $model->id = static::generatePrefixedUlid();
            }
        });
    }

    /**
     * Initialize the trait.
     *
     * Disable auto-incrementing and set the ID type to string.
     * Automatically executed when the trait is registered on the model.
     */
    public function initializeHasPrefixedUlid(): void
    {
        $this->incrementing = false;
        $this->keyType = 'string';
    }

    /**
     * Generate a new ULID with the model's prefix.
     */
    public static function generatePrefixedUlid(): string
    {
        return Str::lower(static::resolveUlidPrefix() . '_' . (string) Str::ulid());
    }

    /**
     * Resolve the ULID prefix (STRICT POLICY A).
     *
     * Every model MUST define:
     *   protected static string $ulidPrefix = 'abc';
     *
     * Where the prefix is exactly 3 lowercase letters.
     *
     * @throws \RuntimeException
     */
    protected static function resolveUlidPrefix(): string
    {
        $prefix = static::$ulidPrefix;

        if (!is_string($prefix) || preg_match('/^[a-z]{3}$/', $prefix) !== 1) {
            throw new RuntimeException(sprintf(
                '%s must define a valid ULID prefix: protected static string $ulidPrefix = \'abc\'; (exactly 3 lowercase letters).',
                static::class
            ));
        }

        return $prefix;
    }
}
```

**Enforcement rule:**

- If any model is generated without:
  - `use HasPrefixedUlid;`
  - AND without `protected static string $ulidPrefix = 'abc';`
    then the implementation is INVALID.

---

## API vs Web Rules (STRICT)

### API Routes

- MUST be versioned:
  - `/api/v1/`
  - `/api/v2/`
  - etc.
- MUST follow strict REST naming conventions:
  - `GET    /api/v1/posts`
  - `POST   /api/v1/posts`
  - `GET    /api/v1/posts/{post}`
  - `PATCH  /api/v1/posts/{post}`
  - `DELETE /api/v1/posts/{post}`

#### Action-based API endpoints (EXTREMELY RARE)

- Only permitted when no RESTful alternative is considerably clean.
- If used:
  - MUST be `POST`
  - Must represent a meaningful domain action
  - Prefer REST alternatives first (usually `PATCH`).
- Example (discouraged unless necessary):
  - `POST /api/v1/posts/{post}/deactivate`
- Preferred REST alternative:
  - `PATCH /api/v1/posts/{post}` with a state change

### Web Routes

- Web routes (`routes/web.php`) do NOT need versioning.
- Web controllers can return views/redirects and do NOT require JsonResources.

---

## Controller Namespacing & Directory Structure (MANDATORY)

Controllers MUST match route structure.

### API Controller Structure

- Route: `/api/v1/posts`
  - Controller: `Api/V1/PostsController`
  - File: `app/Http/Controllers/Api/V1/PostsController.php`
  - Namespace: `App\Http\Controllers\Api\V1`

### Nested Resources

- Route: `/api/v1/posts/{post}/comments`
  - Controller: `Api/V1/Posts/CommentsController`
  - File: `app/Http/Controllers/Api/V1/Posts/CommentsController.php`
  - Namespace: `App\Http\Controllers\Api\V1\Posts`

### Requests & Resources Versioning (API only)

- API Form Requests MUST be versioned:
  - `app/Http/Requests/Api/V1/`
- API Resources MUST be versioned:
  - `app/Http/Resources/Api/V1/`

---

## Response Rules

### API Endpoints

- MUST return `JsonResource` or `ResourceCollection`.
- MUST NOT return raw Eloquent models directly from controllers.

### Web Endpoints

- Do NOT require JsonResources.
- Return views/redirects as appropriate.

---

## Code Structure & Readability Rules (CRITICAL)

### 1) No Nested If Statements

- Nested `if` statements are a code smell and are prohibited.
- Use guard clauses and early returns to flatten control flow.

### 2) Avoid Else Blocks

- Prefer early returns and guard clauses.
- Structure code so `else` is unnecessary.

### 3) Nested Loops Policy

- Nested loops are a smell but not banned.
- Allowed only when:
  - Bounded
  - The simplest and most readable solution
  - Does not introduce unbounded time/space complexity
- Do NOT overengineer abstractions just to avoid nested loops.

### 4) Prefer Laravel Collections

- Favor Collections over `foreach`/`for` loops for succinctness and capability.
- Use `map`, `filter`, `reduce`, `each`, `firstWhere`, `groupBy`, etc.
- Use loops only when they are clearly more readable or necessary.

### 5) No Hard Instantiation

- Do NOT instantiate classes directly inside other classes (e.g. `new SomeService()`).
- Use dependency injection or container resolution.

#### Exception (dynamic constructor arguments)

- If a dependency requires runtime-specific args, evaluate whether it should be:
  - Passed into the method that needs it (method injection), instead of being a constructor dependency.
- Avoid injecting dynamic/ephemeral values via constructors when they are only needed for one operation.

---

## Third-Party Service Rules (MANDATORY)

All third-party services MUST:

1. Be configured in `config/services.php`
2. Use environment variables
3. Be registered in the service container
4. Be injected (never directly instantiated)

Controllers MUST NOT directly call third-party SDKs.
Wrap third-party SDK interactions in a service class and register that service in the container.

---

## Core Architecture Rules

### Controllers

- Thin orchestration only:
  - Validate -> Authorize -> Domain/App logic -> Response

### Validation

- Always use Form Requests for write operations.
- Always use `$request->validated()` (never `$request->all()` for persistence).

### Authorization

- Use Policies or Gates for protected resources.
- Do not embed authorization logic in controllers.

### Domain Logic Placement

- Models: simple aggregate behavior only
- Actions/Services: multi-step workflows, cross-model operations, reuse
- Jobs: long-running or retryable work
- Events: only when they meaningfully reduce coupling

### Dependency Injection

- Prefer constructor injection for stable dependencies.
- Prefer method injection for runtime-specific dependencies.

---

## Database & Migrations

- Use transactions for multi-write operations where partial failure would corrupt state.
- Avoid N+1 queries; eager load relationships when returning collections.
- Add appropriate indexes and foreign keys.
- Ensure `down()` migrations are correct.
- Use casts and enums intentionally (enums only in `app/Enums`, manually created).

---

## API Error Standards

| Status | Meaning |
|--------|---------|
| 422 | Validation errors |
| 401 | Unauthenticated |
| 403 | Unauthorized |
| 404 | Not found |
| 409 | Conflict |

Never leak sensitive fields.

---

## Testing Requirements

Defaults:

- Feature tests for HTTP endpoints
- Unit tests for pure logic

Minimum coverage for new behavior:

- Happy path
- Validation failure
- Authorization failure (if applicable)
- One meaningful edge case

Queues/Events:

- Fake and assert dispatch/listener behavior.

Use factories for test data.
Tests must pass.

---

## AI Implementation Rules

If implementing AI functionality:

- MUST use `laravel/ai`
- NEVER use provider SDKs directly
- Consult Context7 + official docs:
  https://laravel.com/docs/12.x/ai-sdk.md
- Keep prompts structured and maintainable
- Prefer configuration-driven providers
- Keep AI orchestration injectable and testable

---

## Anti-Patterns (Prohibited)

- Nested `if` statements
- Unbounded nested loops
- Direct class instantiation within other classes
- Repository pattern by default
- Premature service layers
- Unversioned API routes
- Returning raw models from API controllers
- `$table->id()`, `$table->foreignId()`, `$table->ulid()`
- Using JsonResources for web routes unless explicitly needed
- Direct provider SDK usage for AI (must use `laravel/ai`)

---

## Output Format (STRICT)

When generating code/changes, output in this order:

1. Assumptions (only if needed)
2. Artisan Commands (to scaffold)
3. Plan (file-by-file)
4. Implementation (grouped by file path)
5. Commands to run (tests, migrations, lint)
6. Definition-of-Done checklist

---

## Definition of Done (Self-Verify)

- [ ] Context7 consulted
- [ ] Artisan used for scaffolding (except enums)
- [ ] Enums manually created in `app/Enums`
- [ ] HasPrefixedUlid trait exists at `app/Models/Concerns/HasPrefixedUlid.php` and matches canonical implementation
- [ ] Every model uses `HasPrefixedUlid`
- [ ] Every model defines `protected static string $ulidPrefix` (3 lowercase letters)
- [ ] `$table->string('id')->primary()` used everywhere
- [ ] No `$table->id()`, `$table->foreignId()`, `$table->ulid()`
- [ ] All foreign keys are strings with explicit foreign constraints
- [ ] Framework default migrations adjusted to string IDs/FKs
- [ ] API routes versioned (`/api/v1`, `/api/v2`, etc.)
- [ ] REST conventions followed
- [ ] Action endpoints avoided; if used, POST only and justified
- [ ] Controller namespaces and directories match routes (including nested resources)
- [ ] API Requests/Resources versioned
- [ ] JsonResource/ResourceCollection used for API endpoints only
- [ ] No nested `if` statements
- [ ] No unnecessary `else` blocks
- [ ] Nested loops only when bounded and simplest solution
- [ ] Collections used where appropriate
- [ ] No direct instantiation; dependencies injected or container-resolved
- [ ] Third-party services configured in `config/services.php` and registered in container
- [ ] Validation uses Form Requests and `$request->validated()`
- [ ] Authorization present where required
- [ ] No N+1 introduced
- [ ] Transactions used where needed
- [ ] Tests added/updated and passing
- [ ] If AI used: `laravel/ai` used per official docs

---

## Clarification Policy

Only ask questions if ambiguity materially affects architecture.
Otherwise choose the most conventional Laravel approach and state assumptions briefly.
