# Requests for comments (RFCs)

**A template for managing technical decisions via version control.**

This repository is the home of the Requests for Comments (RFC) process for [Project Name]. It is a permanent, chronological archive of the architecturally significant technical decisions made over the lifetime of the project, and the mechanism by which those decisions are proposed, discussed, and accepted or rejected.

<!--

The RFC format {link-nytimes}[originated in 1969] in the ARPANET project, the forerunner of the Internet. RFCs remain in use to this day, primarily at the {link-ietf-rfcs}[Internet Engineering Task Force] and other IT standardization organizations. In this domain RFCs are used principally to facilitate technical standardization efforts and to document industry best practices.

-->

A Request for Comments (RFC) is a proposal for a _significant_ technical change. Many changes — bug fixes, documentation tweaks, routine refactors — are handled through the normal pull-request workflow of the relevant code repository. But some changes are substantial enough that it is worth building consensus on the design _before_ implementation. That is what the RFC process is for.

> [!IMPORTANT]
> RFCs cover technical decisions — _how_ the system is built. Product decisions – about _what_ the system should do – are tracked separately in the [software requirements specification (SRS)](https://github.com/kieranpotts/specs). Both the RFC and SRS repositories are managed via similar workflows, but different stakeholders are involved. RFCs originate from technical stakeholders, while the SRS is maintained by product managers.

Changes that typically warrant an RFC include:

- Changes to the system architecture and data models, or significant deviations from established implementation patterns.

- Changes to the technology stack, production infrastructure, or major dependencies.

- Changes to interfaces — graphical, command-line, or programmatic — or anything with significant downstream impact.

- Changes that may affect a service level agreement, such as the security model or features that carry performance or availability risk.

- Changes to development or operations tools and lifecycle processes — anything that affects how contributors do their work.

- Changes to coding conventions and other technical standards.

The serialized RFC documents form a continuous, chronological log of all the major technical decisions made over the history of this project.

## Contents

- [**RFCs**](./rfc/): The permanent archive of every technical decision, including those that were ultimately rejected. The [`index`](./rfc/INDEX.md) lists all accepted, rejected, and superseded RFCs. The[`template`](./rfc/TEMPLATE.md) is the starting point for a new RFC.

- [**Contributing**](./CONTRIBUTING.md): Step-by-step instructions to pitch technical proposals and shepherd them through the RFC process.

- [**Agents**](./AGENTS.md): Instructions for agentic tools to manage the RFC workflow with a high degree of autonomy.

<!--

- [**Documentation**](./docs/): Further guidance on how to get the most out of the RFC process, including how to scope RFCs, how to write good RFCs, and how to manage the RFC process in a way that maximizes its benefits.

-->

-----

Copyright © 2020-present Kieran Potts, [CC0 license](./LICENSE.txt)

**Acknowledgements**: The concept of Requests for Comments originates from the IETF's RFC process, which is specified in [RFC 2026](https://www.rfc-editor.org/rfc/rfc2026.txt). The design of this RFC template has been influenced by [Ember's RFCs](https://github.com/emberjs/rfcs), [ESLint's RFCs](https://github.com/eslint/rfcs), [React's RFCs](https://github.com/reactjs/rfcs), [Rust's RFCs](https://rust-lang.github.io/rfcs/) and [Major Change Proposals](https://forge.rust-lang.org/compiler/mcp.html), [Vue's RFCs](https://github.com/vuejs/rfcs), [Yarn's RFCs](https://github.com/yarnpkg/rfcs), [Java Specification Requests](https://www.jcp.org/en/jsr/overview) and [Architectural Decision Records (ADRs)](https://www.youtube.com/watch?v=rwfXkSjFhzc) – the [ADRs for HashiCorp's unified web docs project](https://github.com/hashicorp/web-unified-docs/tree/main/docs/decisions) providing a good example of how to apply the ADR format.
