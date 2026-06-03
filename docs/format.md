# RFC format

RFCs should be centralized and may be implemented in databases or software systems like wikis. But starting with a code repository with an integrated code review tool – as implemented in this repository – is RECOMMENDED. These tools will already be familiar to development teams, which reduces the learning curve and encourages adoption. Using code repositories also keeps the log of technical decisions close to the code and configuration that those decisions impact.

When using a version control system like Git to implement RFCs, the RFC workflow ends up being similar to the normal software development workflow. When someone wants to propose an idea, they create a branch in the RFC repository, write their idea in a text document, and commit it to the upstream repository. A request for comments is initialized by opening a pull request. The pull request can be commented on by anyone with access to the RFC repository. Alternatively, chat systems can be used as forums for design discussions. Through the PR system the proposal is peer reviewed and iterated upon, exactly the same way that code changes are moderated.

Ultimately, whether a proposal is accepted or rejected, the RFC document is merged into the main branch. With the PR closed, the RFC process is concluded for that particular proposal.

At an early stage of a greenfield project, the filesystem of the main branch of the RFC repository might look something like this:

```
.
├─ rfc/
│  └─ tooling/
│     └─ git-for-version-control/
│        └─ README.md
└─ README.md
```

Side branches capture proposals — one proposal per branch. On merge, the RFC is assigned a sequential number – RFC 1, RFC 2, etc.

It is RECOMMENDED to start with a lightweight RFC system like this, then iterate on its design as you learn more about what works and what doesn't within the context of your organization. The RFC process can be made more lightweight or more heavyweight, as appropriate for the business domain of the software under development. It should also be adjusted as appropriate for the experience level of the team members.

Of course, the RFC system is a great tool for managing the evolution of the RFC system itself!

Over time, you may find it necessary to introduce features such as taxonomies and full-text searches. Other features to consider include integrations with chatops and notification systems, fine-grained access controls, and document versioning. Tools can be introduced to automate recurring steps of the RFC process — the Rust project has its own [rfcbot](https://rfcbot.rs/) — but it is recommended to keep it manual to start, then automate once the process has settled into a regular pattern.

One potential downside of using a version control system for RFCs is that the technical decision-making process will be less accessible to non-technical stakeholders. It may be beneficial to have separate RFC-like systems for higher-level business-oriented decisions and lower-level technical decisions.
