_Copy the "Summary" section from the RFC document here._

- Discussion thread: [Link] _(REQUIRED)_

> [!IMPORTANT]
> Please use the discussion thread linked above, not comments on this pull request, to provide feedback on this proposal. This will keep the PR thread focused on the edit history of the proposal document, while the discussion thread serves as the forum for all review feedback.

----

## Checklist

The author(s) of the RFC MUST update this checklist as their proposal moves through its lifecycle. They MUST NOT merge this PR before the proposal is final — either `IMPLEMENTED` (an accepted decision whose tooling and infrastructure are now in place) or `REJECTED`. An accepted RFC stays open through implementation. See the [contributing guidelines](../CONTRIBUTING.md) for more details about state transitions for RFCs.

Checklist for opening a new pull request:

- [ ] The PR should be opened as a draft, initially.
- [ ] Add one category label: `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`.
- [ ] Open a discussion thread. Link to it above.
- [ ] Update the RFC document with links to this PR and the discussion.
- [ ] Set the RFC document's `Status` to `DRAFT`.

Checklist for transitioning from `DRAFT` to `PROPOSED`:

- [ ] The proposal is complete enough to invite stakeholder review.
- [ ] There is no placeholder text remaining in the proposal document.
- [ ] The RFC document's `Status` is updated to `PROPOSED`.
- [ ] The PR is marked "ready for review" (taken out of draft status).
- [ ] The `#proposed` label is applied to the PR.

Checklist for transitioning from `PROPOSED` to `ACCEPTED` or `REJECTED`:

- [ ] Feedback is gathered from all relevant stakeholders.
- [ ] The main points of contention are resolved.
- [ ] All stakeholders are aligned on the outcome.
- [ ] The proposed solution has stabilized.
- [ ] Final comments have been solicited for at least ___ days.
- [ ] The RFC has not materially changed during this time.
- [ ] The RFC document's `Status` is `ACCEPTED` or `REJECTED`.
- [ ] The `#proposed` label is removed from the PR.
- [ ] Either the `#accepted` or `#rejected` label is applied to the PR.

Checklist for an `ACCEPTED` RFC — keep this PR open through implementation, then transition to `IMPLEMENTED`:

- [ ] Blocking RFCs (`Depends on`) are resolved.
- [ ] Implementation trackers are created and referenced, if applicable.
- [ ] The tooling and infrastructure the decision calls for are in place.
- [ ] The RFC document reflects the decision as actually carried out.
- [ ] The RFC document's `Status` is updated to `IMPLEMENTED`.
- [ ] The `#accepted` label is removed and `#implemented` applied.

Checklist for merging the PR (a `REJECTED` RFC merges straight away; an `IMPLEMENTED` one merges here):

- [ ] Squash-merge the PR, with a message of the form `rfc: <description> - IMPLEMENTED|REJECTED`.
- [ ] Close the discussion thread.

After merge:

- [ ] Add the RFC to `rfc/INDEX.md`, with next sequential number.
