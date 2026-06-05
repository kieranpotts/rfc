# Use Git for version control

- Authors: Kieran Potts [@kieranpotts]
- Created: 2024-01-12
- Last updated: 2024-02-20
- Approvers: Kieran Potts
- Approval date: 2024-01-26
- PR: #1
- Discussion thread: https://github.com/kieranpotts/rfc/discussions/1

## Status

IMPLEMENTED

## Related RFCs

None — this is the project's first RFC.

## Implementation trackers

None.

## Summary

Adopt Git as the version control system for all of the project's source code and documentation, hosted on a single remote forge, with a trunk-based branching model. This establishes the foundation on which the rest of the development and operations lifecycle is built.

## Motivation

The project needs a version control system before any meaningful collaboration can begin. The choice affects every contributor on every working day, and it constrains the tooling — code review, continuous integration, release automation — that we layer on top. It is therefore a foundational technical decision worth recording explicitly, even though the outcome is uncontroversial.

We need: reliable history, cheap branching to support parallel work, strong support for distributed and asynchronous collaboration, and a large ecosystem of compatible tooling and hosting providers.

## Impact

HIGH

This decision affects every contributor and underpins all subsequent process and tooling decisions — code review, CI/CD, release management, and the branching conventions that govern day-to-day work. Getting it wrong, or changing it later, would be disruptive and costly.

## Proposed state

All source code and documentation will be managed in [Git](https://git-scm.com/) repositories. We will:

- Use Git for distributed version control, with one repository per deployable unit or cohesive documentation set.

- Host repositories on a single remote forge (separate decision), to centralize code review, issue tracking, and automation in one place.

- Adopt a trunk-based branching model: short-lived feature branches cut from a single long-lived main branch, and merged back via pull request. Detailed branching, merging, and release conventions will be settled in follow-up RFCs.

Repository hygiene — `.gitignore`, `.gitattributes` for line-ending normalization, and commit-message conventions — will be standardized across all repositories.

## Alternatives

**Mercurial**: A capable distributed VCS with a reputation for a cleaner CLI. Rejected because Git's ecosystem — hosting, CI providers, tooling, and the prevailing familiarity among contributors — is materially larger, which lowers onboarding cost and operational risk.

**A centralized VCS (e.g. Subversion)**: Rejected because centralized systems handle branching and offline/asynchronous work poorly, which is a bad fit for distributed collaboration and fast, continuous integration workflows.

## Trade-offs and risks

- **Learning curve**: Git's model and CLI are notoriously unintuitive for newcomers. Mitigated by standardizing conventions and providing tooling and documentation, addressed in follow-up RFCs.

- **Large binary assets**: Git handles large binaries poorly. If the project later needs to version large media, a mechanism such as Git LFS will need its own RFC.

## Questions

- Which specific branching-and-merging convention should we adopt? Deferred to a follow-up RFC.

- Which remote forge and CI provider? Deferred to a follow-up `TOOLING` RFC.

## References

- [Pro Git book](https://git-scm.com/book/en/v2)
