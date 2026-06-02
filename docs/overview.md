# Overview of the RFC process

A good RFC process steers each technical decision through a series of distinct lifecycle phases. This repository uses the following phases:

- **Draft**: A preliminary version of a proposal, put forward for early feedback. This step is optional — a proposal may be opened directly as `Proposed`.

- **Proposed**: A proposal that is being negotiated with the relevant stakeholders.

- **Accepted**: A proposal that has been approved and is queued for implementation.

- **Rejected**: A proposal that has been rejected and will not be taken forward.

- **Superseded**: A previously accepted proposal that is no longer in effect, having been replaced by a more recent one.

The RFC process is initialized by a proposal being put forward for comments — literally, a request for comments. Proposals are negotiated with the relevant stakeholders. During this phase, the original proposal may change, perhaps significantly, in response to stakeholder feedback. Once a solution is agreed, the proposal is updated to describe the settled solution, the design rationale for it, and the relative pros and cons of any alternative solutions that were considered.

The outcome of the RFC process is for the finalized proposal to be either accepted or rejected.

When a proposal is accepted, it is queued for implementation. Tasks may be created in the relevant project management tools to track the implementation.

Thereafter, the contents of the original RFC documents are treated as immutable. To change past decisions, new RFCs must be introduced that supersede the originals. Previously-accepted RFCs that are no longer in effect are marked as superseded.

Records of all past decisions — even those that are no longer in effect or were rejected in the first place — are preserved indefinitely, providing an accurate reflection of the technical evolution of the project. This also makes it easier to maintain the decision log over time. The immutable state of past decision documents means they do not need to be kept up-to-date. Only new proposals are editable, and in time these will be relatively few compared to the total number of prior decisions.
