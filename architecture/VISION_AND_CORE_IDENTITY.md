# Architectural Vision & Core Identity

## 1. Vision & Complete Architectural Independence
* **The Ecosystem:** Ugarit Ecosystem (**إطار ومنظومة أوغاريت**).
* **Vision Leader:** **Muath R Abu Ouda** (`muathrabuouda@hotmail.com`).
* **Philosophical Foundation:**
  * Ugarit is an independent, Arabic-first web application framework built and developed as a derivative work from Laravel, maintaining complete compliance with original IP rights and the MIT License.
  * **Strict Isolation Law:** It is strictly prohibited to pull, require, or import any legacy packages (`laravel/*` or `illuminate/*`) from Packagist or any external repository into the Ugarit ecosystem.
  * The core framework is completely self-contained under the official GitHub and Packagist organizations `ugarit` and `ugaritco`.

---

## 2. Architectural Mapping & Official Terminology

| Concept / Component | Official Ugarit Name | Namespace / Details |
| :--- | :--- | :--- |
| **Framework Package** | `ugarit/framework` | Official core package |
| **Vendor Organizations** | `ugarit` & `ugaritco` | Official GitHub & Packagist organizations |
| **Core Namespace** | `Heritage\...` | Core classes namespace (replaces `Illuminate\...`) |
| **CLI Tool** | `scribe` | Command line tool invoked via `php scribe` |
| **Brand Name** | `Ugarit` / `ugarit` | Official ecosystem brand name |
| **Application Kernel** | `Heritage\Foundation\Application` | Central service orchestrator & router |
| **Testing Engine** | `Pest` via `ugaritco/pest-plugin-ugarit` | Default test suite runner |
| **Static Analysis** | `ugaritco/ugaritstan` | Official static analysis tool |
| **Code Formatter** | `ugarit/pint` | Dedicated isolated code cleaner |

---

## 3. Versioning Standard (`1.00.00`)
* All packages and repositories across the Ugarit ecosystem adhere to the unified versioning format: **`v1.00.00`** (two-digit sub-version format).
* Incremental progress evolves as:
  `v1.00.01` ➔ `v1.00.02` ➔ `v1.00.03` ... and so forth.
* All legacy repository tags (`v5.x`, `v4.x`, etc.) must be permanently purged to avoid Packagist dependency resolution conflicts.
