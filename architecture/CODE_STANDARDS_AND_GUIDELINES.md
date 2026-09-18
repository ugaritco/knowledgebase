# Ugarit Code Standards & Engineering Guidelines

> [!IMPORTANT]
> **The Engineering Law of Ugarit:**
> Every line of code written across the **Ugarit Ecosystem** and its **Artifacts** must satisfy the highest standards of software craftsmanship. This guide synthesizes **Clean Code principles**, the **LevantC layer-isolation doctrine**, and our **Mandatory Commenting Mandate**.

---

## 1. The Core Engineering Mandates

1. **The Mandatory Commenting Rule ("لا كود بدون تعليق يوضحه"):**
   * **No code may exist without clear, explanatory comments.**
   * Every file, class, interface, method, and non-trivial logical block must be accompanied by comprehensive docblocks and explanatory inline comments.
2. **Clean Code & SOLID Foundations:**
   * Methods must be small, focused, and perform exactly one logical task.
   * Classes must honor the **Single Responsibility Principle (SRP)**.
   * Deep nesting is prohibited: use guard clauses and early returns.
3. **Strict Layer Isolation (LevantC Standard):**
   * Controllers never execute business logic or database queries.
   * Repositories strictly encapsulate Eloquent models and map them to DTOs; models never leak past repository boundaries.
   * UseCases encapsulate discrete operations and return standardized **Outcome** envelopes.
4. **Architectural Sovereignty:**
   * Strictly zero imports of legacy framework symbols (`Illuminate\*`, `Laravel\*`). All core code uses `Heritage\*`.
   * Every PHP file must declare strict types: `declare(strict_types=1);`.

---

## 2. The Mandatory Commenting Standard

Code must explain its **intent**, **responsibilities**, and **context**. Writing code without explanatory comments is strictly prohibited.

### 2.1 Class-Level PHPDoc (Mandatory)
Every class, interface, enum, and trait must have a comprehensive header explaining:
1. What the class represents.
2. Which architectural layer it belongs to (Controller, UseCase, Repository, DTO, etc.).
3. How it interacts with surrounding components.

```php
<?php

declare(strict_types=1);

namespace Ugarit\Artifacts\Geography\Services\UseCases;

use Ugarit\Artifacts\Geography\Contracts\CountryRepositoryContract;
use Ugarit\Artifacts\Geography\DTOs\SaveCountryDTO;
use Ugarit\Artifacts\Geography\Outcomes\GeographyOutcome;
use Ugarit\Artifacts\Geography\Signals\CountryCreatedSignal;

/**
 * Class SaveCountryUseCase
 *
 * Layer: Domain / Operation (UseCase)
 *
 * Responsible for validating business rules, persisting country records
 * through the CountryRepository, emitting the CountryCreatedSignal, and
 * returning a standardized GeographyOutcome envelope.
 */
class SaveCountryUseCase
{
    // ...
}
```

---

### 2.2 Method-Level PHPDoc & Signatures (Mandatory)
Every method must include:
1. A concise description of the operation.
2. Full `@param` descriptions with semantic context.
3. A `@return` description explaining the expected outcome.
4. `@throws` annotations for any checked or runtime exceptions.

```php
    /**
     * Persist a country entity and emit domain signals.
     *
     * @param  SaveCountryDTO  $dto  The validated data transfer object carrying country attributes.
     * @return GeographyOutcome      The standardized result envelope with persisted data and client feedback.
     */
    public function handle(SaveCountryDTO $dto): GeographyOutcome
    {
        // 1. Persist country entity through repository boundary
        $saved = $this->repository->save($dto);

        // 2. Broadcast domain signal to notify listeners of country creation
        event(new CountryCreatedSignal($saved));

        // 3. Assemble and return successful outcome envelope
        return GeographyOutcome::success(
            data: $saved->toArray(),
            message: "Country [{$saved->name}] persisted successfully."
        );
    }
```

---

### 2.3 Step-by-Step Inline Comments (Mandatory)
Inside method bodies, developers and AI Agents must write step-by-step explanatory comments that explain the **why** and **what**:
* Detail validation or verification criteria.
* Clarify data mapping and transformations.
* Highlight safety checks, edge cases, and transaction boundaries.

```php
    public function findByIso(string $iso): ?CountryDTO
    {
        // Normalize ISO code to uppercase to prevent collation mismatches
        $normalizedIso = strtoupper(trim($iso));

        // Query database via either Alpha-2 (2 letters) or Alpha-3 (3 letters) standard
        $model = Country::query()
            ->where('iso_alpha_2', $normalizedIso)
            ->orWhere('iso_alpha_3', $normalizedIso)
            ->first();

        // If no matching record exists, safely return null without throwing
        if (! $model) {
            return null;
        }

        // Map private Eloquent model attributes to immutable DTO before exiting boundary
        return CountryDTO::fromArray($model->toArray());
    }
```

---

## 3. Clean Code & Structural Guidelines

### 3.1 Strict Typing & Explicit Signatures
Every PHP file must start with `declare(strict_types=1);`. Every method parameter and return type must be explicitly declared. Mixed or untyped signatures are forbidden unless strictly required by an external contract.

```php
// ❌ FORBIDDEN: Untyped signature
public function find($id) { ... }

// ✅ MANDATORY: Strictly typed signature
public function findById(int $id): ?CountryDTO { ... }
```

---

### 3.2 Guard Clauses & Early Returns (No Deep Nesting)
Avoid nested `if/else` structures ("The Arrow Anti-Pattern"). Validate preconditions first and return early:

```php
// ❌ FORBIDDEN: Deeply nested conditions
public function handle(SaveLocaleDTO $dto): I18nOutcome
{
    if ($dto->isActive) {
        if ($this->repository->findByCode($dto->code) === null) {
            $saved = $this->repository->save($dto);
            return I18nOutcome::success($saved);
        } else {
            return I18nOutcome::failure('Duplicate code');
        }
    } else {
        return I18nOutcome::failure('Inactive locale');
    }
}

// ✅ MANDATORY: Guard clauses and early returns
public function handle(SaveLocaleDTO $dto): I18nOutcome
{
    // Precondition 1: Ensure locale is active
    if (! $dto->isActive) {
        return I18nOutcome::failure('Inactive locale cannot be registered.');
    }

    // Precondition 2: Guard against duplicate locale code
    if ($this->repository->findByCode($dto->code) !== null) {
        return I18nOutcome::failure("Locale with code [{$dto->code}] already exists.");
    }

    // Happy Path: Execute persistence
    $saved = $this->repository->save($dto);

    return I18nOutcome::success($saved);
}
```

---

### 3.3 Immutability by Default
Data Transfer Objects (DTOs) and Outcomes must be immutable using `readonly class`:

```php
// ✅ MANDATORY: Immutable DTO
readonly class LocaleDTO
{
    public function __construct(
        public int $id,
        public string $code,
        public string $name,
        public TextDirection $direction,
        public bool $isDefault = false,
    ) {}
}
```

---

## 4. LevantC-Derived Layer Invariants

```text
HTTP Request
    │
    ▼
[Controller]           ──► Zero business logic; assembles DTO; invokes UseCase
    │
    ▼
[UseCase / Operation]  ──► Executes business rules; interacts via Repository Contract
    │
    ▼
[Repository Boundary]  ──► Executes Eloquent query; maps Model to DTO (Models NEVER leak)
    │
    ▼
[Signal]               ──► Emits domain occurrence notification
    │
    ▼
[Outcome Envelope]     ──► Standardized agnostic result envelope
    │
    ▼
[Responder]            ──► Adapts Outcome to Transport (JSON / Inertia / Redirect)
```

### Layer Rules Checklist:
1. **Controllers:**
   * Never contain `Model::where(...)` or database operations.
   * Only receive inputs, build DTOs, execute UseCases, and pass the Outcome to a Responder.
2. **UseCases (Operations):**
   * Single responsibility: One use case handles one action (e.g., `SaveCityUseCase`, `DestroyLocaleUseCase`).
   * Interacts with repositories strictly via **Contracts** (Dependency Inversion).
   * Emits **Signals** upon state changes.
   * Returns a typed **Outcome** envelope.
3. **Repositories (Data Boundary):**
   * Never leak Eloquent Model instances past the repository boundary.
   * All queries must return DTOs or collections of DTOs (`Collection<int, DTO>`).
4. **Responders:**
   * Sole responsibility is translating the agnostic `Outcome` to HTTP transport (JSON response, Inertia props, CLI output).
   * Zero business logic.

---

## 5. Automated Quality & Tooling Gates

Before committing any code or issuing a release:

1. **Syntax Check:**
   ```bash
   php -l <path-to-file.php>
   ```
2. **Code Style & Formatting (`ugarit/pint`):**
   ```bash
   vendor/bin/pint
   ```
3. **Automated Testing Suite (Pest):**
   ```bash
   php scribe test
   ```
4. **Git Conventional Commits:**
   ```bash
   git commit -m "type(scope): imperative summary"
   ```
