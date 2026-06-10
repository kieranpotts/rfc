# Scope of RFCs

RFCs are most commonly used to record critical choices made in the _design_ of an IT system. In this regard, RFCs are conceptually equivalent to key design decisions (KDDs) and architectural decision records (ADRs).

But there is no limit to the possible scope of RFCs. There is no reason why they can't be used to support any kind of technical decision, anything that impacts how a system is made, such as:

- Adoption of design patterns and coding conventions.
- Choices of languages, frameworks, and libraries.
- Development and operations processes, and related automation tools (eg. CI/CD).
- Policies such as branching-and-merging strategies and test-and-release plans.
- Project management practices and ways of working.

The scope of RFCs could be anything that would benefit from collective decision making among technical stakeholders, or where it would be beneficial to reach agreement on a solution to a problem as far "left" as possible in the development lifecycle.

Anything that will have a significant impact on how a system is made, or that will be of interest to more than one group of technical stakeholders, or that will change the context in which future technical decisions will be made, is a candidate for an RFC.

Large IT functions will benefit from a centralized RFC system for standardizing tools and methods across the organization, and for reaching agreement on how to implement changes that will impact multiple work streams. Meanwhile, individual teams may have their own internal RFC systems for making decisions over which they have autonomy.

Each proposal put forward for comments should be scoped to a single technical decision. But the breadth of impact may be broad or narrow, and the range of stakeholders involved should be proportional to that impact. Refactoring the internal structure of a discrete module should require input from just a few technical people. Replacing a language in the technology stack, or adding a major new tool to the delivery pipeline, should require broad consensus from many more people.

And proposals that could affect service level agreements or mission alignment may need to be elevated to product owners or other business stakeholders. Not all RFCs may be isolated to the technical domain.

The widest possible scope for RFCs would be to use them to evaluate proposals for functional and non-functional requirements. This certainly makes sense in the context of software libraries and other software components, where the users are other software developers. But at larger scales – in enterprise application software development, for example – it tends to be preferable to keep technical decisions reasonably isolated from product decisions. That means having alternative processes to capture, refine, and prioritize product ideas. A [software requirements specification (SRS)](https://github.com/kieranpotts/specs) if perfect for this use case.
