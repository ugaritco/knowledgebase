# Documentation Standards & Guidelines

Extracted from the **LevantC Core** architecture and adapted as the official documentation standard across the **Ugarit Ecosystem**.

Every repository, module, and package within Ugarit must adhere to this unified documentation framework to guarantee clarity, modular scalability, and seamless onboarding for both human engineers and AI Agents.

---

## 1. The Standard Repository Documentation Suite

Every module or repository in the ecosystem must provide a standardized documentation suite consisting of the following core documents:

```text
repository-root/
├── README.md              # Primary entry point & ecosystem orientation
├── ARCHITECTURE.md        # Deep architectural design, DDD layers & request flows
├── CONTRIBUTING.md        # Contribution workflows, commit conventions & PR guidelines
├── INSTALLATION.md        # Comprehensive installation, configuration & verification
├── OVERVIEW.md            # High-level vision, core philosophy & problem definition
├── ROADMAP.md             # Development milestones & planned capabilities
├── SECURITY.md            # Security policy & vulnerability reporting protocol
├── CODE_OF_CONDUCT.md     # Community and contributor code of conduct
├── CONTACT.md             # Maintainer and official contact channels
└── LICENSE.md             # Official MIT License honoring Muath R Abu Ouda
```

---

## 2. Document-by-Document Specification

### A. `README.md` Specification
The `README.md` serves as the primary storefront and orientation guide. It must contain:
1. **Title & Badge Header:** Official package name (`vendor/package`), version badge, build status.
2. **Executive Summary:** A concise 2–3 paragraph summary defining what the package is, who it is for, and why it exists.
3. **Role in the Ecosystem:** A Markdown table defining the layer and responsibilities:
   ```markdown
   | Layer | Package | Responsibility |
   |---|---|---|
   | **Kernel** | `ugarit/framework` | Core service container and foundation |
   | **Artifact** | `ugaritco/<artifact>` | Autonomous capability package |
   ```
4. **Core Capabilities:** Bulleted breakdown of technical capabilities provided by the Artifact.
5. **Architecture Mapping Table:** Directory-to-layer correspondence (Controllers, DTOs, Services, Repositories, Outcomes, Signals, etc.).
6. **Quick Start / Installation:** Minimal commands to require and register the module.
7. **Standards & Testing:** Reference to code formatting, Pint, Pest test commands, and Conventional Commits.
8. **Vision Leader & License:** Official attribution to **Muath R Abu Ouda** and MIT license link.

---

### B. `ARCHITECTURE.md` Specification
The `ARCHITECTURE.md` must clearly define the technical blueprint and data flow:
1. **Foundation Model & Separation:** Explanation of how the artifact connects to the core application without framework-inside-a-framework bloat.
2. **Artifact-Driven Architecture (ADA) Layers:**
   ```markdown
   | Layer | Responsibility | Rule |
   |---|---|---|
   | **DTOs** | Structured data transfer | Explicit typed input and output shapes |
   | **Repositories** | Persistence abstraction | Map Eloquent to DTOs; never leak raw models past repository boundaries |
   | **Services / Use Cases** | Business orchestration | Handle domain operations; emit Signals; return standardized Outcome envelopes |
   | **Contracts** | Interface abstractions | Explicit shared interfaces in `src/Contracts/` |
   | **Http / Controllers** | HTTP routing & dispatch | Delegate exclusively to Use Cases; zero business rules |
   | **Responders** | Transport adaptation | Translate Outcome envelopes into JSON, Inertia, CLI, or Redirects |
   | **Outcomes** | Standardized outcome | Encapsulate data payload, status, and user feedback metadata (replaces Response) |
   | **Signals** | Domain notifications | Broadcast-ready domain notification of occurrences (replaces Event) |
   | **Actions** | User-facing feedback | Actionable UI descriptors (toasts, alerts, side effects) |
   ```
3. **Request Flow Pipeline Diagram (Mermaid):**
   ```text
   HTTP Request
       → Controller
           → UseCaseFactory → UseCase::handle(DTO)
               → Signal::emit(DomainSignal)
               → Outcome (data, toast, result semantics)
           → ResponderFactory → Responder (JSON | Inertia | Redirect)
       → HTTP Response
   ```
4. **Repository File Tree:** Complete visual directory tree explaining all namespaces and directories.
5. **Autoloading & Discovery:** PSR-4 mapping and `art.php` manifest registration mechanics.
6. **Scalability Principles:** Horizontal artifact growth, independent repository versioning, and stable extension points.

---

### C. `CONTRIBUTING.md` Specification
The `CONTRIBUTING.md` establishes engineering quality gates:
1. **Scope of Repository:** Explicit definition of what belongs in this repository vs. upstream/downstream packages.
2. **Branch Strategy:**
   * `main` — Production-ready, stable release branch.
   * `1.x` — Active development and patch tracking branch.
   * `develop` — Integration branch for incoming features.
   * Feature branches: `feat/<feature-name>`, `fix/<issue-name>`.
3. **Commit Convention (Conventional Commits):**
   ```text
   type(scope): Short and clear description
   ```
   * Types: `feat`, `fix`, `refactor`, `docs`, `test`, `chore`.
4. **Pre-PR Testing & Code Style:**
   * Test execution: `php scribe test` or Pest suite runner.
   * Code formatting: `vendor/bin/pint` (`ugarit/pint`).
   * Adherence to PSR-12 and PSR-4.
5. **Architecture Consistency Rules:** Clear prohibitions (e.g., controllers performing database queries, models bypassing repositories).

---

### D. `INSTALLATION.md` Specification
Step-by-step onboarding guide:
1. **Prerequisites:** PHP version (`^8.2`), Ugarit Framework compatibility.
2. **Package Requirement:** `composer require "ugaritco/<package>:^1.00.00"`.
3. **Configuration Publishing:** Command to publish module configuration and environment variables.
4. **Database Migrations:** Running migrations via `php scribe migrate`.
5. **Verification Step:** Health check command or test suite verification.

---

### E. `OVERVIEW.md` & `ROADMAP.md` Specification
* **`OVERVIEW.md`:** Focuses on the "Why" and "What" from a systemic perspective. Explains the core architectural philosophy, decoupling benefits, and high-level architectural overview.
* **`ROADMAP.md`:** Transparent tracking of releases:
  * Milestone phases (Phase 1: Foundation, Phase 2: Domain Capabilities, Phase 3: Enterprise Scale).
  * Status badges: Completed, In Progress, Planned.

---

### F. `SECURITY.md`, `CONTACT.md` & `CODE_OF_CONDUCT.md`
* **`SECURITY.md`:** Strict directive against public issue reports for vulnerabilities; provides designated contact `muathrabuouda@hotmail.com`.
* **`CONTACT.md`:** Leadership contact information, GitHub Discussions link, and contribution queries.
* **`CODE_OF_CONDUCT.md`:** Standard Contributor Covenant emphasizing respectful, constructive collaboration.

---

## 3. Core Principles for AI Agents Generating Documentation

When an AI Agent is tasked with generating or updating documentation for any Ugarit package:
1. **No Missing Documents:** Ensure all 9 standard documents exist and maintain identical formatting.
2. **Strict Terminology:**
   * Use `Ugarit` and `Heritage\...`.
   * Never reference legacy Laravel or Illuminate namespaces in public guides.
   * Tool references must use `scribe` (not artisan).
3. **Mermaid Diagrams:** Include Mermaid diagrams for data flows, component hierarchies, and state machines.
4. **Code Quality:** All code examples in markdown must be syntactically valid PHP 8.2+ or shell commands with proper escaping.
