# Requests for Comments (RFC)

**A template for managing technical decisions via version control.**

This repository is the home of the Requests for Comments (RFC) process for [Project Name]. It is a permanent, chronological archive of the architecturally significant technical decisions made over the lifetime of the project. It is also the mechanism by which new technical decisions are proposed, discussed, and accepted or rejected.

RFCs cover technical decisions — _how_ the system is built. Product decisions – about _what_ the system should do – are tracked separately in the [software requirements specification (SRS)](https://github.com/kieranpotts/specs). Both the RFC and SRS repositories are managed by the technical teams and follow similar change management workflows.

## Contents

- [**RFCs**](./rfc/): The permanent archive of every technical decision, including those that were ultimately rejected.

  - The [`INDEX`](./rfc/INDEX.md) lists all implemented, rejected, and superseded RFCs. (Current proposals being discussed are tracked via the [pull requests](https://github.com/kieranpotts/rfc/pulls) system.)

  - The [`TEMPLATE`](./rfc/TEMPLATE.md) is the starting point for a new RFC.

- [**Contributing**](./CONTRIBUTING.md): Step-by-step instructions to pitch technical proposals, and to shepherd them through the RFC process.

- [**Agents**](./AGENTS.md) and [**Skills**](./.agents/skills/): Instructions for agentic tools to manage the RFC workflow with a high degree of autonomy.

- [**Documentation**](./docs/): Further guidance on how to get the most out of the RFC process.

-----

Copyright © 2020-present Kieran Potts, [CC0 license](./LICENSE.txt)
