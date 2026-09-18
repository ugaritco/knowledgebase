# AI Agents Constitution & Operating Guidelines

> [!IMPORTANT]
> **Absolute Golden Rule:**
> This constitution is binding for every AI Agent operating within the Ugarit ecosystem. No task may be executed without full compliance with this guide.

---

## 1. Operating Principles
1. **Knowledge-First Entry:**
   * Before undertaking any task, the agent must review the architectural specifications documented in the `knowledgebase` repository.
2. **Absolute Architectural Independence:**
   * It is strictly prohibited to require or import any legacy packages (`laravel/*` or `illuminate/*`).
   * The core framework classes must reside exclusively under the `Heritage\...` namespace, published under `ugarit` and `ugaritco`.
3. **Unified Versioning Standard:**
   * All new packages and repositories must begin at version **`v1.00.00`**, following the two-digit minor/patch progression (`v1.00.01`, `v1.00.02`, etc.).
   * Inherited legacy tags must be purged immediately to prevent Composer/Packagist resolution errors.
4. **Windows Console & PowerShell Escaping:**
   * Escape shell special characters (specifically wrapping constraints with `^` in double quotes).
   * Enforce `--no-interaction` flags on automated installer commands.
   * Guard against multibyte character corruption on Windows OEM code pages (e.g., CP-720).
5. **Cache Clearing & Packagist Synchronization:**
   * After updating packages or tags: immediately run `composer clear-cache`, push all tracking branches (`main`, `1.x`, `develop`), and trigger instant Packagist API synchronization.
