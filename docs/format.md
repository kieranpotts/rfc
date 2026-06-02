# RFC format

<!--

RFCs should be centralized and may be implemented in databases or software systems like wikis. But I recommend starting with a code repository with an integrated code review / merge request tool. These tools will be already familiar to the development teams. This will reduce the learning curve, encourage adoption, and it will keep the log of technical decisions close to the relevant code and configuration.

I've created a *{link-template-rfcs}[template RFC repository in GitHub]*, which you can fork to get started. That repository's README has a step-by-step guide to the RFC process, but I'll summarize it here:

When someone wants to propose an idea, they will create a branch in the RFC repository, write their idea in a text document, and commit it to the upstream repository. A request for comments is initialized by opening a pull request. The pull request can be commented on by the relevant stakeholders. Alternatively, linked chat systems can be used to undertake the design discussions. Through the PR system the proposal is peer reviewed and iterated upon, exactly the same way that code changes are reviewed.

Ultimately, whether the proposal is accepted or rejected, the RFC document will be merged into the main branch. With the PR closed, the RFC process is shut down for that particular proposal.

At an early stage of a greenfield project, the filesystem of the main branch of the RFC repository might look something like this:

----
.
├─ rfcs/
│  ├─ 0001-git-for-version-control.md
│  ├─ 0002-github-for-code-repository-hosting.md
│  ├─ 0003-trunk-based-source-control-workflow.md
│  ├─ 0004-nodejs-runtime-for-api-gateway.md
│  └─ TEMPLATE.md
│
└─ README.md
----

Side branches would capture proposals. There should be one proposal per branch. Thus, the contents of a branch named `proposal/express-for-http-abstraction` might looks like this:

----
.
├─ rfcs/
│  ├─ 0001-git-for-version-control.md
│  ├─ 0002-github-for-code-repository-hosting.md
│  ├─ 0003-trunk-based-source-control-workflow.md
│  ├─ 0004-nodejs-runtime-for-api-gateway.md
│  ├─ express-for-http-abstraction.md
│  └─ TEMPLATE.md
│
└─ README.md
----

Once a proposal is merged into the main branch, it should be given a unique identifier. By convention, this is an auto-incrementing integer. This is recommended because the order in which proposals get added to the main branch is significant:

----
.
├─ rfcs/
│  ├─ 0001-git-for-version-control.md
│  ├─ 0002-github-for-code-repository-hosting.md
│  ├─ 0003-trunk-based-source-control-workflow.md
│  ├─ 0004-nodejs-runtime-for-api-gateway.md
│  ├─ 0005-express-for-http-abstraction.md
│  └─ TEMPLATE.md
│
└─ README.md
----

A template should be included for new proposals. I recommend keeping it simple to start. Use a lightweight text markup format such as Markdown, AsciiDoc or Textile, and request that the following key information be captured:

* *Context*: The forces at play – the functional and non-functional requirements, and constraints such as time, budget and expertise – that shaped the proposed solution.

* *Solution*: This section may evolve over the course of an RFC's lifecycle. Ultimately, the final agreed or rejected solution should be captured, and also the final implemented solution if the design further evolved during construction.

* *Alternatives*: The relative pros and cons of any alternative solutions that were considered by the RFC author or by contributors during design discussions.

* *Consequences*: What are the trade-offs (the costs versus the benefits) of the proposed solution, as they were understood at the time? This should cover both positive and negative consequences, and "known unknown" outcomes.

*{link-proposal-tpl}[Here's an example template.]*

I recommended starting with a lightweight RFC system like this, then iterating on its design as you learn more about what works and what doesn't work within the context of your organization. The RFC process can be made more lightweight or more heavyweight, as appropriate for the business domain of the software under development. It should also be adjusted as appropriate for the experience level of the team members.

Of course, the RFC system is a great tool for managing the evolution of the RFC system itself!

Over time, you may find it necessary to introduce features such as taxonomies and full-text searches. Other features to consider include integrations with chatops and notification systems, fine-grained access controls, and document versioning. Tools can be introduced to automate recurring steps of the RFC process – the Rust project has its very own https://rfcbot.rs/[rfcbot] – but it is recommended to keep it manual to start, then automate once the process has settled into a regular pattern.

One potential downside of using a version control system for RFCs is that the technical decision making process will be less accessible to non-technical stakeholders. It may be beneficial to have separate RFC-like systems for higher-level business-oriented decisions and lower-level technical decisions.

-->
