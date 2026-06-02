# Overview of the RFC process

<!--

In this section I propose a simple and lightweight RFC process that you can use as a starter kit for introducing RFCs to your project. First I'll describe the process at a conceptual level. Then I'll propose a concrete implementation based around the most ubiquitous development tool of them all – Git.

A good RFC process will steer each technical decision through a series of distinct lifecycle phases. As a starting point, I suggest the following phases:

* *Draft*: A preliminary version of a proposal, put forward for early feedback. This step is optional.

* *Proposed*: A proposal that is being negotiated with the relevant stakeholders.

* *Accepted*: A proposal that has been approved and is currently pending implementation.

* *Rejected*: A proposal that has been rejected and will not be taken forward.

* *Implemented*: A proposal that has been implemented and is currently in effect in production systems.

* *Deprecated*: A legacy proposal that was previously accepted and implemented but has since been superseded by more recent changes and is no longer in effect.

The RFC process is initialized by a proposal being put forward for comments – literally, a request for comments. Proposals are negotiated with the relevant stakeholders. During this phase, the original proposal may change, perhaps significantly, in response to stakeholder feedback. Once a solution is agreed, the proposal is updated to describe the settled solution, the design rationale for it, and the relative pros and cons of any alternative solutions that were considered.

The outcome of the RFC process is for the finalized proposal to be either accepted or rejected.

When a proposal is accepted, it is queued for implementation. Tasks may be created in the relevant project management tools to track the implementation. (You might introduce an additional "pending" phase here, to indicate an accepted proposal that has been transferred to the product backlog.)

Thereafter, the contents of the original RFC documents are treated as immutable. Therefore, to change past decisions, new RFCs will need to be introduced that extend or supersede prior ones. Previously-approved RFCs that are no longer in effect, having been superseded by newer ones, are marked as deprecated.

Records of all past decisions – even those that are no longer in effect or were rejected in the first place – are persisted indefinitely and so provide an accurate reflection of the technical evolution of the project. This also makes it easier to maintain the decision log over time. The immutable state of past decision documents means they do not need to be kept up-to-date. Only new proposals are editable, and in time these will be relatively few compared to the total number of prior decisions.

-->
