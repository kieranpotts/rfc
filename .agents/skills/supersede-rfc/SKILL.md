---
name: supersede-rfc
description: >-
  Supersede a previously-implemented RFC with a newer one. Use this skill when
  the user says something like "supersede this RFC", "this RFC is replaced
  by ...", "supersede RFC", "<topic> is superseded by <successor>", or
  otherwise wishes to retire an implemented decision in favor of a newer one.
  Do not use this skill to author the successor RFC.
compatibility: >-
  requires Read, Edit, Glob, Grep, Bash (git, gh)
license: CC0-1.0
---

# Supersede RFC

Transition an RFC from `IMPLEMENTED` to `SUPERSEDED`, once a later,
implemented RFC has replaced its decision. Cross-reference the two documents,
update the index row, and relabel the old pull request. The superseded
document stays in `rfc/` permanently as part of the historical record.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **The superseded RFC — REQUIRED.** The implemented RFC being retired.
  Infer it from the user's description (eg. "X is superseded by Y"), locating
  its row in the index and its document under `rfc/<category>/<slug>/`.

- **The successor RFC — REQUIRED.** The later implemented RFC that replaces
  the decision. Infer it from the same description, or prompt for it.

## Success criteria

- The superseded document's `Status` field MUST be `SUPERSEDED`,
  `Last updated` MUST be today's date, and `Superseded by` MUST name the
  successor by its index number.

- The successor document's `Supersedes` field MUST name the superseded RFC by
  its index number.

- The superseded RFC's row in `rfc/INDEX.md` MUST read `SUPERSEDED`.

- The superseded RFC's original pull request MUST carry `#superseded`
  alongside its category label, and MUST NOT carry `#implemented`.

- All three file changes MUST have been committed directly to `main` in one
  commit, and pushed. No branch or pull request MUST have been opened, and no
  other field of either document MUST have changed.

## Instructions

1.  Identify both RFCs.

    Establish which implemented RFC is being retired and which later
    implemented RFC replaces it. If the user gave a short description (eg. "X
    is superseded by Y"), use it to infer both; otherwise prompt the user.

    Resolve each document from [the RFC index](../../../rfc/INDEX.md), which
    maps a number to a directory. Where only a topic is known, grep `rfc/`
    for the matching document.

2.  Verify the rules.

    Read both documents and check each rule below. Report any failure and
    stop without changing anything.

3.  Update the successor.

    Set its `Supersedes` field to name the superseded RFC by its index
    number.

4.  Update the superseded RFC.

    - Set its `Superseded by` field to name the successor by its index
      number.
    - Set its `Status` field to `SUPERSEDED`.
    - Set `Last updated` to today's date.

    Change nothing else in either document — both are merged, and so
    otherwise immutable.

5.  Update the index.

    In [the RFC index](../../../rfc/INDEX.md), change the superseded RFC's
    row status to `SUPERSEDED`. Leave the successor's row alone.

6.  Land the change.

    Commit both documents and the index row together, directly to `main`, and
    push. Both RFCs are already merged, and every field touched here is one
    of the few a merged RFC may still change — so there is nothing for a pull
    request to review:

    ```sh
    git checkout main
    git pull --rebase
    git commit -am "supersede: <short lowercase description of superseded rfc>"
    git push
    ```

    The push is mandatory. An unpushed supersession leaves the archive
    claiming the old RFC is still in effect.

7.  Switch the lifecycle label on the superseded RFC's original pull request.

    ```sh
    gh pr edit <number> --add-label "#superseded" --remove-label "#implemented"
    ```

    Leave the category label in place, eg. `ARCHITECTURE`.

8.  Report what you did, naming both RFCs by their index numbers.

## Rules

- You MUST NOT supersede an RFC that is not currently `IMPLEMENTED`.

  A draft, proposed, accepted, or rejected RFC has no decision in effect to
  retire. To abandon a decision without replacing it, draft a new RFC that
  says so.

- The successor MUST itself be `IMPLEMENTED`.

  Its replacement tooling and infrastructure have to be in place before the
  old decision stops being in effect. Otherwise the archive describes a gap
  where neither decision applies.

- Both RFCs MUST already be merged into `main` and MUST each carry a unique
  number in [the RFC index](../../../rfc/INDEX.md).

  Supersession is a relationship between two settled records, expressed by
  index number, so both numbers have to exist.

- The successor MUST be the newer of the two, carrying the higher index
  number.

- The change MUST be committed directly to `main` and pushed, not routed
  through a pull request.

  The fields this skill touches — `Status`, `Last updated`, `Superseded by`,
  `Supersedes`, and the index row — are among the few a merged RFC may still
  change, so a pull request would have nothing to review. This matches how
  RFC numbers are assigned when an RFC is merged, which also commits straight
  to `main`.

- You MUST NOT change any field of either document other than `Status`,
  `Last updated`, `Superseded by`, and `Supersedes`.

  Everything else in a merged RFC — the problem, the settled solution, and
  its rationale — is immutable.

- You MUST NOT author the successor RFC.

  This skill records a relationship between two RFCs that already exist. A
  successor that has not been written yet has to go through the full
  lifecycle first.

## Edge cases

- The direct push to `main` in step 6 is rejected by branch protection.

  Where `main` is protected against direct pushes even though both RFCs are
  already merged and settled, open a small pull request carrying the same
  commit instead, merge it immediately, and tell the user this fallback was
  needed, since it means `main` is protected in a way this skill did not
  expect going in.
