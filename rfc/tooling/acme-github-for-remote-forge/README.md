# Use GitHub as the remote forge

> [!NOTE]
> This is a sample RFC, included to illustrate the format. It describes a
> fictional decision for a fictional project ("acme") and is not one of this
> project's real decisions.

- Authors: Jane Doe [@janedoe]
- Created: 2026-02-02
- Last updated: 2026-02-18
- Decided by: Jane Doe
- Decision date: 2026-02-18
- PR: #8
- Discussion thread: https://github.com/acme/rfc/discussions/8

## Status

IMPLEMENTED

## Related RFCs

- Supersedes —
- Superseded by —
- Depends on 0001
- Related to —

## Implementation trackers

- acme/platform#12

## Summary

Host all acme repositories on GitHub, using GitHub Actions as the primary CI
provider, deferred from [RFC 0001](../../tooling/git-for-version-control/).

## Motivation

RFC 0001 established Git as the version control system but explicitly
deferred the choice of remote forge and CI provider. The team needs a
single, centralized place for code review, issue tracking, and automation
before any repository can be created.

## Impact

HIGH

Affects every contributor and every repository. Also determines which CI/CD
integrations, branch-protection mechanisms, and third-party tooling are
available going forward.

## Current state

No remote forge is currently in use; all work happens in local Git
repositories with manual patch sharing.

## Proposed state

Host all repositories on GitHub, under a single `acme` organization. Use
GitHub Actions for CI/CD, GitHub's built-in code review (pull requests) for
change management, and GitHub Issues for tracking. Branch protection rules
will require passing CI and at least one review before merge to `main`.

## Alternatives

**GitLab (self-hosted):** Offers more control over infrastructure, but
introduces an ongoing hosting and maintenance burden the team is not
resourced for.

**Bitbucket:** Comparable feature set, but a materially smaller ecosystem of
third-party integrations and community familiarity.

## Trade-offs and risks

- **Vendor lock-in:** Moving off GitHub later would require migrating issues,
  PR history, and Actions workflows. Accepted as a reasonable trade for the
  lower operational overhead today.

- **Cost at scale:** GitHub's per-seat pricing may become a factor as the team
  grows. Revisit if headcount materially increases.

## Questions

None outstanding.

## References

- [GitHub Actions documentation](https://docs.github.com/actions)
