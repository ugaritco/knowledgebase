# Sources & Reference Blueprints Guide

> [!IMPORTANT]
> **Source-Driven Architecture Rule:**
> AI Agents and developers must rely on reference sources placed in the `sources/` directory (e.g., `sources/levantc`) as architectural and functional blueprints when designing and building custom features for Ugarit.

---

## 1. The `sources/` Directory Philosophy
* **Dynamic Reference Repository:**
  * The `sources/` folder serves as a local incubator for reference systems, architectures, and libraries.
  * New sources can be attached at any time via:
    1. Direct Git repository clones under `sources/<vendor-or-project>`.
    2. External URLs and documentation links recorded in `sources/SOURCES_CATALOG.md`.
* **Decoupled Architectural Ingestion:**
  * Source code in `sources/` is strictly treated as reference blueprints.
  * Code is not copied blindly as third-party vendor dependencies; instead:
    1. The AI Agent inspects design patterns, schemas, interfaces, and lifecycles.
    2. The capabilities are natively re-engineered to seamlessly fit `Heritage\...` architecture.
    3. All terminology and code conventions strictly honor Ugarit guidelines and Arabic localization excellence.

---

## 2. Primary Reference Source: `levantc` Organization
All 14 repositories of the `levantc` GitHub organization have been cloned locally into [`j:\ugarit\sources\levantc`](file:///j:/ugarit/sources/levantc).

| Reference Module | Domain / Specialty | Architectural Target in Ugarit |
| :--- | :--- | :--- |
| **`levantc`** | Foundational Core | Modular service binding and extension points |
| **`i18n`** & **`i18n-ui`** | Internationalization | Comprehensive Arabic-first RTL/LTR linguistic engine and UI |
| **`identity`** | Identity & Access Management | Granular RBAC, modern authentication, and multi-tenancy |
| **`storage`** | Media & File Management | Unified media library, transformations, and multi-disk pipelines |
| **`geography`** | Geo Data & Administrative Units | High-precision global and MENA regions, cities, and currencies |
| **`classification`** | Taxonomies & Tagging | Multi-level tree categories (nested sets) and polymorphic tags |
| **`attributes`** | Dynamic Custom Fields (EAV) | Runtime schema extensions using JSON columns and typed attributes |
| **`content`** | Content Management | Dynamic block-based content publishing and rendering |
| **`registry`** | Component & Service Registries | Distributed registry patterns for modular extensions |
| **`versioning`** | Entity Revision History | Audit trails, visual diffs, and point-in-time entity recovery |
| **`console`** | CLI Helpers | Custom `scribe` console components and commands |
| **`laravel-starter-kit`** | Scaffolding Template | UX patterns for starter kits and onboarding flows |
| **`documentation`** | Architectural Docs | Blueprint for developer documentation and API guides |

---

## 3. AI Agent Source Ingestion Protocol
When assigned to develop or customize an ecosystem feature:
1. **Explore:** Inspect the relevant blueprint module in `sources/` to understand contracts, traits, migrations, and service providers.
2. **Analyze:** Extract the architectural essence and database schemas.
3. **Elevate & Implement:** Build the native Ugarit implementation adhering to `Heritage\...` conventions and the Ugarit Ecosystem Guidelines.
