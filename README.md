# 💬 Requests for Comments (RFC)

**A template for managing technical decisions via version control.**

This repository is the home of the Requests for Comments (RFC) process for [Project Name]. It is a permanent, chronological archive of the architecturally significant technical decisions made over the lifetime of the project. It is also the mechanism by which new technical decisions are proposed, discussed, and accepted or rejected.

RFCs cover technical decisions – _how_ the system is built. Product decisions – about _what_ the system should do – are tracked separately in the [software requirements specification (SRS)](https://github.com/kieranpotts/specs). Both the RFC and SRS repositories are managed by the technical teams and follow similar change management workflows.

## Ecosystem

This repository is one of four that form a coherent, version-controlled documentation ecosystem modeling the software development lifecycle. Each is the reference implementation of an opinionated workflow, and answers a different question about the system:

- [**📋 Software requirements specification (SRS)**](https://github.com/kieranpotts/specs): Records _what_ the system does, in business terms.

- **💬 Requests for comments (RFC)**: Records _how_ significant technical decisions were made, and _why_ (this repository).

- [**📐 Design docs**](https://github.com/kieranpotts/design): Describe _what the system looks like_, its as-is architecture.

- [**🗺️ Implementation plans**](https://github.com/kieranpotts/plans): Capture _when, and in what order_, the work gets done.

The [**skills**](https://github.com/kieranpotts/skills) collection provides an agentic workflow that operates across all four.

This separation into dedicated repositories is intended for application software that spans multiple code repositories, and potentially multiple teams, where the requirements, decisions, designs, and plans are shared concerns that sit above any single codebase. For a standalone code repository – a small utility library, say – it is better to fold these artifacts and skills directly into that repository, rather than maintain them separately.

## Contents

- [**RFCs**](./rfc/): The permanent archive of every technical decision, including those that were ultimately rejected.

  - The [`INDEX`](./rfc/INDEX.md) lists all implemented, rejected, and superseded RFCs. (Current proposals being discussed are tracked via the [pull requests](https://github.com/kieranpotts/rfc/pulls) system.)

  - The [`TEMPLATE`](./rfc/TEMPLATE.md) is the starting point for a new RFC.

- [**Contributing**](./CONTRIBUTING.md): Step-by-step instructions to pitch technical proposals, and to shepherd them through the RFC process.

- [**Agents**](./AGENTS.md) and [**Skills**](./.agents/skills/): Instructions for agentic tools to manage the RFC workflow with a high degree of autonomy.

- [**Documentation**](./docs/): Further guidance on how to get the most out of the RFC process.

-----

Copyright © 2020-present Kieran Potts, [CC0 license](./LICENSE.txt)
