# Overview of the RFC process

The RFC format [originated in 1969](https://www.nytimes.com/2009/04/07/opinion/07crocker.html) in the ARPANET project, the forerunner of the Internet. RFCs remain in use to this day, most notably at the [Internet Engineering Task Force](https://www.rfc-editor.org/rfc/rfc2026.txt) where RFCs facilitate technical standardization efforts across the whole IT industry.

RFCs are also widely used in open source projects – examples include [Ember](https://github.com/emberjs/rfcs), [ESLint](https://github.com/eslint/rfcs), [React](https://github.com/reactjs/rfcs), [Vue](https://github.com/vuejs/rfcs), [Yarn](https://github.com/yarnpkg/rfcs), [Rust RFCs](https://rust-lang.github.io/rfcs/) and [Major Change Proposals](https://forge.rust-lang.org/compiler/mcp.html), and [Java Specification Requests](https://www.jcp.org/en/jsr/overview).

The RFC format is also closely related to the concept of key design decisions (KDDs) and [Michael Nygard’s architectural decision records (ADRs)](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions.html) framework. The [ADRs for HashiCorp's unified web docs project](https://github.com/hashicorp/web-unified-docs/tree/main/docs/decisions) are a good example.

An RFC – or an ADR – is a discrete technical proposal, usually written as a single design document, that justifies an architecturally significant decision. A collection of chronologically-ordered RFCs forms a technical decision log.

The RFC process is initialized by a technical proposal being put forward for comments — literally, a "request for comments" (RFC).

During this initial phase, the proposal is negotiated with relevant stakeholders. The original proposed solution may change, perhaps significantly, in response to stakeholder feedback. Once a solution is agreed, the proposal document is updated to describe the settled solution, the design rationale for it, and the relative pros and cons of any alternative solutions that were considered.

Rejected proposals are also recorded.

The outcome of the RFC process is for a finalized technical proposal that is either accepted or rejected. Either way, the decision is logged.

A common convention is for RFCs to become immutable once they are accepted or rejected. Thereafter, RFCs may only be superseded by newer ones. Thus, records of all past technical decisions — even those that are no longer in effect, having been superseded, or that were rejected in the first place — are preserved indefinitely.

For more background on the RFC process, follow the [related links](./related-links.md).
