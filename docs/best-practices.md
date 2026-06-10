# Best practices

Whatever format and tools you choose to implement your RFC system, here are some universal best practices to optimize the process.

There should be one main document per proposal, and each proposal should be scoped to a single technical decision. RFCs work best when they are kept short, but an arbitrary cap on length should not be set. Some decisions will naturally require more detail. RFC documents can be augmented with diagrams and tables, and linked to mock-ups and prototypes, as appropriate.

Technical writing is an important skill that contributors will need to learn to engage in the RFC process. RFC documents should be written in an informal, conversational tone, as though talking through an idea to a new developer who has no prior knowledge of the system under development – RFCs are NOT formal specifications. Proposals should be written in full sentences organized into paragraphs, and with a consistent information architecture (ie. the same headings in the same order).

Where RFCs are used as a technical design process, they should be tightly coupled with the project's task tracking system. For example, where the implementation of a user story requires substantive revisions to either the external interfaces or the internal construction techniques of a software component, or to its dependencies, it can be beneficial to put the changes through a more rigorous and structured design process _before_ the changes are introduced in code and configuration. Breaking out the work to an RFC is an excellent method for that. Shifting left the design review means that multiple possible designs can be considered, pre-implementation. By contrast, only one option can be considered in code review, post-implementation.

Code review is easier too. The reviewer should already expect a certain design for an implementation, so they're only checking it meets the functional and non-functional requirements, and not also whether it's the optimal design.

RFCs should record conceptual choices as well as concrete details. "We elected to implement a loosely-coupled monolith because…" describes the rationale for one aspect of a system's conceptual architecture. "We decided to use the Hibernate ORM for DB abstraction because…" describes the rationale for a concrete implementation of a specific component of that system. In the grand scheme of a software project, the first example has the farthest-reaching consequences.

The RFC process is about slowing down development so that good decisions are made earlier. The trick is to add _just enough_ friction. How much friction is appropriate will vary. Low-risk and low-cost decisions can be quickly resolved, perhaps through delegation to individual contributors. High-risk or high-cost decisions, which will be more expensive to change later in the development lifecycle, should have more up-front design and planning, perhaps even with spikes or prototypes done as part of the RFC process.

As a general rule, the greater the potential impact of the proposal, the longer the RFC should be open for comments and the more stakeholders should be involved in the decision.

But all RFCs, whatever their scope, should be open to comments from the widest possible range of stakeholders. Junior developers should be encouraged to engage in major architectural decisions, while architects and senior developers should watch over more granular, lower-level details. This encourages more points of view, maximizing the input of knowledge into decisions. It helps to disperse knowledge more widely, reducing silos. And it builds a culture of collaboration, inclusivity, and transparency, helping teams to grow into effective, cohesive units, and nurturing tomorrow's technology leaders.

Technical decisions should be taken by technical people and business decisions by business people. But there can be unexpected benefits to getting cross-domain input into decisions. Technical people learn to communicate their ideas in terms of business value, and non-technical people get useful insights into technical details and an appreciation of the true costs of delivering the business objectives.

From time to time the most insightful comments on technical proposals have come from non-technical people, and junior developers have been known to propose simpler, but equally effective, alternatives to solutions proposed by seasoned architects.

Perspective is as important as expertise. It's not unusual for obvious risks and flaws in a design to be spotted only by the people furthest from the problem.

Psychological safety is key to the success of the RFC process. Everyone should be encouraged to put forward ideas, safe in the understanding that the team will collectively own any final decision and individuals will not be blamed for unexpected negative consequences. A culture of psychological safety permits teams to take risks and to learn from mistakes.

If decisions are to be made by consensus, then there needs to be a framework in place for reaching consensus. Who has a vote over which types of decision, and who gets the casting vote in deadlock situations? When and how should decisions be elevated to higher authorities? The decision-making framework should be set out in the context of a wider technical strategy and guiding principles that inform the direction of the project.

RFCs require a strong governance model. RFCs are all about consensus-based decision making, but decisions will need to be taken by an authority in situations where consensus cannot be found. The design authority would normally be a technical lead or architect, and in the context of a bottom-up decision-making environment they would ideally operate in a [benevolent dictator](https://github.com/git-for-windows/git-for-windows.github.io/blob/main/governance-model.md#benevolent-dictator-project-lead) capacity.

Finally, it is worth stating that no method or tool in software development is a [silver bullet](https://en.wikipedia.org/wiki/No_Silver_Bullet), and RFCs are no exception. They will not work in every organization. Introducing RFCs to a development process will work only in settings with an already-established culture of trust, autonomy, and responsibility. And the benefits of consensus-based decision making need to be carefully balanced against the risks. Beware of falling into the trap of design-by-committee. An over-engineered RFC process can be unnecessarily slow and bureaucratic, and not actually produce better outcomes.
