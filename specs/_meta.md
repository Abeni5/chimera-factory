---
description: Metadata for Project Chimera Specifications
---

# Project Chimera Specifications Metadata

This directory (`specs/`) contains all ratified specifications for Project Chimera. All development (code generation, modification, testing) MUST adhere strictly to these specifications, as per the [Prime Directive in .cursor/rules/project_chimera.mdc](../../.cursor/rules/project_chimera.mdc).

## Specification Types:

-   **`functional.md`**: High-level functional requirements and user stories, directly mapping to SRS.
-   **`technical.md`**: Detailed technical designs, API contracts, data models (Pydantic), and architectural decisions.
-   **`_meta.md`**: This file, providing context and guidelines for the specifications.
-   **`openclaw_integration.md`**: Specific details regarding the integration with the OpenClaw protocol.

## Guidelines for Use:

1.  **Single Source of Truth**: `specs/` is the authoritative source for all project requirements and design.
2.  **No Vibe Coding**: No implementation or feature development should occur without a corresponding, ratified specification here.
3.  **Ambiguity Resolution**: If a specification is unclear or missing, development must pause, and clarification sought from the Project Lead.
4.  **Version Control**: All changes to specifications must go through standard Git version control (PRs, reviews).
5.  **Traceability**: All code changes or feature implementations should ideally reference the specific section or line number of the relevant specification.