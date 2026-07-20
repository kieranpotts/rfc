# Adopt a trunk-based branching and merging convention

> [!NOTE]
> This is a sample RFC, included to illustrate the format. It describes a
> fictional decision for a fictional project ("acme") and is not one of this
> project's real decisions.

- Authors: John Smith [@johnsmith]
- Created: 2026-03-01
- Last updated: 2026-03-14
- Decided by: Jane Doe
- Decision date: 2026-03-14
- PR: #15
- Discussion thread: https://github.com/acme/rfc/discussions/15

## Status

IMPLEMENTED

## Related RFCs

- Supersedes —
- Superseded by —
- Depends on 0001, 0002
- Related to —

## Implementation trackers

- acme/platform#31

## Summary

Formalize the trunk-based branching and merging convention deferred from
[RFC 0001](../../tooling/git-for-version-control/): short-lived feature
branches cut from `main`, merged via squash-merge pull request.

## Motivation

RFC 0001 committed to a trunk-based model in principle but left the concrete
conventions — branch naming, merge strategy, review requirements — for a
follow-up decision. Without an explicit convention, contributors were
starting to diverge on merge strategy (some merge commits, some rebases),
making history harder to read.

## Impact

MEDIUM

Affects day-to-day contributor workflow and the shape of the commit history,
but is reversible with moderate effort if it proves unworkable.

## Current state

No formal convention exists. `main` is the only long-lived branch, but
branch naming and merge strategy are inconsistent across contributors.

## Proposed state

- Feature and fix branches are cut directly from `main`, named
  `<type>/<slug>`, eg. `feature/checkout-retry`, `fix/webhook-timeout`.

- Branches are short-lived: opened, reviewed, and merged within a few days
  wherever possible, to minimize drift from `main`.

- All merges to `main` use squash-merge, producing one commit per pull
  request, with a commit message matching the PR title.

- Long-lived branches (release branches, epics) are the explicit exception
  and are named `release/*` or `epic/*`.

## Alternatives

**Git flow (develop + release branches)**: Rejected as unnecessary ceremony
for a team shipping continuously rather than in scheduled release trains.

**Merge commits instead of squash**: Rejected because squash-merge keeps
`main`'s history at one commit per unit of reviewed work, which is easier to
bisect and revert.

## Trade-offs and risks

- **Loss of intermediate commit history**: Squash-merge discards the
  in-review commit history. Accepted, since that history is preserved on the
  originating PR for as long as GitHub retains it.

- **Long-lived branches drifting**: Epics and release branches risk drifting
  far from `main` if not actively rebased. Mitigated by requiring periodic
  rebase as part of the epic-branch convention.

## Questions

None outstanding.

## References

- [Trunk Based Development](https://trunkbaseddevelopment.com/)
