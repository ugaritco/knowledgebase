# Ugarit Central Knowledge Base

> [!IMPORTANT]
> **The Single Source of Truth for Developers & AI Agents:**
> This repository serves as the central entry point and architectural compass for all developers and **AI Agents** participating in the development and customization of the Ugarit Ecosystem. No code execution, architectural design, or feature introduction may occur without consulting and strictly aligning with this knowledge base.

---

## 🏛️ Vision & Leadership
* **Vision Leader:** **Muath R Abu Ouda** (`muathrabuouda@hotmail.com`).
* **Strategic Objective:** Build and maintain an independent, Arab-led, world-class web application ecosystem that combines developer ergonomics, architectural robustness, and native Arabic-first localization capabilities.

---

## 🧭 Repository Structure

```text
knowledgebase/
├── README.md                              # Central introduction and directory guide
├── LICENSE.md                             # Official MIT License honoring Muath R Abu Ouda
├── composer.json                          # Package definition
├── architecture/                          # Core architectural documentation
│   ├── UGARIT_PHILOSOPHY.md               # The master philosophy: Artifacts provide capabilities, Features define behavior
│   ├── ARTIFACT_DRIVEN_ARCHITECTURE.md    # Official technical reference for ADA & decoupled frontend
│   ├── VISION_AND_CORE_IDENTITY.md        # Vision, identity, and strict isolation laws
│   ├── ECOSYSTEM_MAP.md                   # Ecosystem topology and package relationships
│   ├── SOURCES_AND_REFERENCES.md          # Source ingestion guide (LevantC & external refs)
│   ├── CUSTOMIZATION_PILLARS.md           # Strategic customization roadmap & pillars
│   ├── DOCUMENTATION_GUIDELINES.md        # Official documentation suite & rules (LevantC Standard)
│   └── VERSIONING_AND_RELEASE_MANAGEMENT.md # Two-digit semver (1.xx.xx) & commit specifications
├── agents/                                # AI Agent guidelines and execution protocols
│   ├── AGENTS_CONSTITUTION.md             # The binding constitution for all AI agents
│   └── INSTRUCTIONS.md                    # Pre-execution workflow & quality gates
└── sources/                               # Reference sources index
    └── SOURCES_CATALOG.md                 # Inventory of blueprint packages (LevantC modules)
```

---

## ⚡ Core Principle: Artifacts vs. Features
> **"Artifacts provide capabilities. Features define behavior."**

1. **Artifacts Provide Capabilities:** Independent technical packages that deliver domain-agnostic capabilities (storage, identity, i18n, attributes).
2. **Features Define Behavior:** Application-level workflows composing capabilities from one or more Artifacts.
3. **The Invariant:** `Feature → Artifact` (Allowed). `Artifact ↛ Feature` (Forbidden).

---

## 📋 Getting Started for AI Agents
All agents must read the following guides in sequence prior to task execution:
1. [`architecture/UGARIT_PHILOSOPHY.md`](architecture/UGARIT_PHILOSOPHY.md)
2. [`architecture/ARTIFACT_DRIVEN_ARCHITECTURE.md`](architecture/ARTIFACT_DRIVEN_ARCHITECTURE.md)
3. [`architecture/VISION_AND_CORE_IDENTITY.md`](architecture/VISION_AND_CORE_IDENTITY.md)
4. [`agents/AGENTS_CONSTITUTION.md`](agents/AGENTS_CONSTITUTION.md)
5. [`sources/SOURCES_CATALOG.md`](sources/SOURCES_CATALOG.md)
