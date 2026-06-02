# RFC format

RFCs should be centralized and may be implemented in databases or software systems like wikis. But starting with a code repository with an integrated code review tool is recommended. These tools will already be familiar to development teams, which reduces the learning curve, encourages adoption, and keeps the log of technical decisions close to the relevant code and configuration.

You can [fork this repository](https://github.com/kieranpotts/rfc) to get started quickly. The README has a step-by-step guide to the RFC process, but here is a summary:

When someone wants to propose an idea, they create a branch in the RFC repository, write their idea in a text document, and commit it to the upstream repository. A request for comments is initialized by opening a pull request. The pull request can be commented on by the relevant stakeholders. Alternatively, linked chat systems can be used to undertake the design discussions. Through the PR system the proposal is peer reviewed and iterated upon, exactly the same way that code changes are reviewed.

Ultimately, whether the proposal is accepted or rejected, the RFC document is merged into the main branch. With the PR closed, the RFC process is concluded for that particular proposal.

At an early stage of a greenfield project, the filesystem of the main branch of the RFC repository might look something like this:

```
.
├─ rfc/
│  ├─ tooling/
│  │  └─ git-for-version-control/
│  │     └─ README.md
│  ├─ INDEX.md
│  └─ TEMPLATE.md
│
└─ README.md
```

Side branches capture proposals — one proposal per branch. On merge, the RFC is assigned a sequential, zero-padded number recorded in `INDEX.md`. The RFC's directory and filename are never renamed; the number lives only in the index:

```
rfc/
├── INDEX.md
├── TEMPLATE.md
├── architecture/
├── process/
├── technology/
└── tooling/
    └── <slug>/
        ├── README.md
        └── …    ← diagrams or other supporting artifacts
```

A template should be included for new proposals. Keep it simple to start. The following key information should be captured:

- **Summary**: A concise description of the proposed decision.
- **Motivation**: The problem and who it affects.
- **Proposed state**: The solution, in enough detail to evaluate.
- **Alternatives**: The relative pros and cons of any alternative solutions that were considered.
- **Trade-offs and risks**: An honest account of the costs, risks, and drawbacks.

[Here's the template used by this repository.](https://github.com/kieranpotts/rfc/blob/main/rfc/TEMPLATE.md)

Start with a lightweight RFC system like this, then iterate on its design as you learn more about what works and what doesn't within the context of your organization. The RFC process can be made more lightweight or more heavyweight, as appropriate for the business domain of the software under development. It should also be adjusted as appropriate for the experience level of the team members.

Of course, the RFC system is a great tool for managing the evolution of the RFC system itself!

Over time, you may find it necessary to introduce features such as taxonomies and full-text searches. Other features to consider include integrations with chatops and notification systems, fine-grained access controls, and document versioning. Tools can be introduced to automate recurring steps of the RFC process — the Rust project has its own [rfcbot](https://rfcbot.rs/) — but it is recommended to keep it manual to start, then automate once the process has settled into a regular pattern.

One potential downside of using a version control system for RFCs is that the technical decision-making process will be less accessible to non-technical stakeholders. It may be beneficial to have separate RFC-like systems for higher-level business-oriented decisions and lower-level technical decisions.
