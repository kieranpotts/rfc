# Requests for comments (RFCs)

**A template for managing technical decisions via version control.**

This repository is the home of the Requests for Comments (RFC) process for [Project Name]. It is a permanent, chronological archive of the architecturally significant technical decisions made over the lifetime of the project, and the mechanism by which those decisions are proposed, discussed, and accepted or rejected.

A Request for Comments (RFC) is a proposal for a _significant_ technical change. Many changes — bug fixes, documentation tweaks, routine refactors — are handled through the normal pull-request workflow of the relevant code repository. But some changes are substantial enough that it is worth building consensus on the design _before_ implementation. That is what the RFC process is for.

Changes that typically warrant an RFC include:

- Changes to the system architecture, or deviations from established implementation patterns.

- Changes to interfaces — graphical, command-line, or programmatic — or anything with significant downstream impact.

- Changes that may affect a service level agreement, such as the security model or features that carry performance or availability risk.

- Changes to development or operations lifecycle processes — anything that affects how contributors do their work.

- Changes to the technology stack or major dependencies.

> [!NOTE]
> This repository covers technical decisions — _how_ the system is built. Product decisions about _what_ the system should do are tracked separately, in the companion [software requirements specification](https://github.com/kieranpotts/specs) repository.

## Contents

- [**RFCs**](./rfcs/): The permanent archive of every proposed technical decision, including those that were ultimately rejected. `TEMPLATE.md` is the starting point for a new RFC.

- [**Contributing**](./CONTRIBUTING.md): Instructions for shepherding an RFC through its lifecycle.

- [**Agents**](./AGENTS.md): Instructions for agentic tools to manage the RFC workflow with a high degree of autonomy.

-----

Copyright © 2020-present Kieran Potts, [CC0 license](./LICENSE.txt)
