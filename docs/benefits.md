# Benefits of the RFC process

The ultimate aim of RFCs is to make better technical decisions.

This is achieved by opening up decision making to the widest possible range of stakeholders. The RFC process is, fundamentally, a system to democratize technical decision-making. The idea is to gather feedback on technical proposals from as many technical stakeholders as possible. If decisions are made collaboratively, absorbing lots of ideas and points of view, the outcomes will be better than if technical decisions are made by a privileged elite from ivory towers.

RFCs make the decision-making process more transparent. Everyone can see how decisions were made and why. Non-technical stakeholders, too, can gain insights from RFCs into the technical direction of a project.

This helps to foster collaborative, inclusive work cultures. RFCs promote consensus-based decision making and empower everyone to make an impact at work — not only the most vocal people. RFCs help to share knowledge, disseminate expertise, and foster inclusive and psychological safety work cultures. Ideas may be put forward by individuals, but the team is collectively accountable for the final agreed decisions. [Research shows](https://dora.dev/) that these conditions are the necessary foundations for the formation of high-performing teams.

RFCs can help individuals to grow their skills, too. The RFC process encourages clarity of thought. The act of putting an idea into writing, and soliciting comments on it from others, requires the author to clearly articulate the problem and their proposed solution, to think through the pros and cons, and to weigh up all the other ways the problem could be solved. These skills are fundamental to system design thinking.

The RFC process discourages impulsive decisions and channels thinking in the direction of long-term solutions. These constraints are particularly important for architecturally significant decisions, or anything that will be costly or risky to implement in the first place, or to change after the fact.

The output from the RFC lifecycle is an immutable decision document or design document. These documents are valuable artifacts in their own right, but more valuable still is a chronologically-ordered collection of them. This serves as a ledger of major technical decisions taken over the lifetime of a project — a technical decision log.

While program code, automated test scripts, architectural diagrams, and other forms of documentation record _what_ a system does and _how_ it does it (the "here and now"), these artifacts do not tell you _why_ a system is made the way it is (the "how we got here"). A technical decision log fills this gap. This knowledge would otherwise risk being lost as the original decision makers gradually offboard from the project.

Recording today's decisions for posterity will mean better decisions can be made in the future. Or, to look at it another way, we could make better decisions now if we understood the context in which past decisions were made. What were the main constraints — eg. time, budget, expertise, or quality requirements such as security and performance — that shaped the current design of the system? What was the rationale for previous technical decisions, and were the consequences fully understood at the time?

When we understand a project's history, we can reevaluate relevant decisions taken in the past when the situation changes. Clearly, it is useful to keep permanent records of why some technical decisions were rejected up front, or subsequently changed or even fully reverted. Future developers won't waste time revisiting the same options. Equally valuable is to understand the motivation for choosing a particular solution over alternative designs, so we don't naively change an implementation and lose the value sought through the original design.

Decision logs give us confidence to refactor code and to continuously improve our development and operations processes. The more detailed the record of past decisions, the greater the confidence teams will have to change them.

RFCs, and the decision records they produce, have many other benefits. For example, RFCs give visibility to the wider contributions of individual team members — beyond fixes, stories, commits, and releases — providing more data points for analysis in personal performance reviews. And they can be used to generate useful metrics related to the wider [technical health](https://engineering.atspotify.com/2023/03/getting-more-from-your-team-health-checks/) of teams and projects. For example, a low RFC participation rate may indicate problems with engagement and trust.

RFCs scale wonderfully well. The immutability of past RFCS means that maintenance overhead does not increase as the decision log gets longer, because only current proposals need to be kept up-to-date. Indeed, the larger the project, the more useful RFCs become. They can be used to facilitate technical standardization and to help share knowledge between multiple teams. They can support asynchronous ways of working, which becomes more necessary as communication overhead grows. RFCs will become more useful still as IT workforces get more geographically distributed and flexible working schedules become more widely supported.
