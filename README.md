# 💬 Requests for Comments (RFC)

**A template for managing technical decisions** via version control.

This repository is the home of the Requests for Comments (RFC) process for
[Project Name]. It is a permanent, chronological archive of the architecturally
significant technical decisions made over the lifetime of the project. It is
also the mechanism by which new technical decisions are proposed, discussed, and
accepted or rejected.

RFCs cover technical decisions – _how_ the system is built. Product decisions –
about _what_ the system should do – are tracked separately in the
[software requirements specification (SRS)](https://github.com/kieranpotts/specs).

RFCs drive choices in the implementation. Those choices show up in the
[design docs](https://github.com/kieranpotts/design).

The RFCs, SRS, and design docs are managed by the technical teams and follow
similar change management workflows.

> [!NOTE]
> See also [TS-3](https://github.com/kieranpotts/standards/tree/latest/dev/src/003),
> a technical standard covering design docs, RFCs, and architecture audits.
> This repository is its reference implementation for RFCs.

## Ecosystem

This repository is one of six that form a coherent, version-controlled
documentation ecosystem. Each answers a different question about a software
system.

- [**📋 Software Requirements Specification (SRS)**](https://github.com/kieranpotts/specs) \
  Captures what the system does today, plus proposals being discussed to change
  the requirements.

- [**📐 Design Docs**](https://github.com/kieranpotts/design) \
  Architectural views representing the as-is production system, plus proposals
  to evolve the architecture to meet new requirements.

- [**🗺️ Delivery Plans**](https://github.com/kieranpotts/plans) \
  Roadmaps, milestones, and the decomposition of work into independently
  shippable increments.

- [**💬 Requests for Comments (RFC)**](https://github.com/kieranpotts/rfc) (this repository) \
  An historical record of key design and technical decisions, plus active
  proposals and their discussion threads.

- [**🔍 Architecture Audits**](https://github.com/kieranpotts/audits) \
  Point-in-time evaluations of the structural integrity of the code and data,
  which drive refactoring work.

- [**⚠️ Risk Register**](https://github.com/kieranpotts/risks) \
  Security and privacy risks inherent in the system, and the implementation
  status of mitigation strategies. Plus an archive of past threat modeling
  workshop reports.

In addition, the [**✨ Agent Skills**](https://github.com/kieranpotts/skills)
collection offers composable agentic workflows that operate across all six
repositories.

This separation into dedicated repositories is intended for application software
that spans multiple code repositories, and potentially multiple teams, where the
requirements, decisions, designs, plans, audits, and risks are shared concerns
that sit above any single codebase.

For a standalone code repository – a small utility library, say – it may be
better to fold all documentation into the same repository.

## Contents

- [**RFCs**](./rfc/) \
  The permanent archive of every technical decision, including those that were
  ultimately rejected.

  - The [`INDEX`](./rfc/INDEX.md) lists all implemented, rejected, and
    superseded RFCs. Current proposals being discussed are tracked via the
    [pull requests](https://github.com/kieranpotts/rfc/pulls) system.

  - The [`TEMPLATE`](./rfc/TEMPLATE.md) is the starting point for a new RFC.

- [**Contributing**](./CONTRIBUTING.md) \
  Step-by-step instructions to pitch technical proposals, and to shepherd them
  through the RFC process.

- [**Agents**](./AGENTS.md) and [**Skills**](./.agents/skills/) \
  Instructions for agents to manage the RFC workflow with a high degree of
  autonomy.

- [**Documentation**](./docs/) \
  Further guidance on how to get the most out of the RFC process.

-----

Copyright © 2020-present Kieran Potts, [CC0 license](./LICENSE.txt)
