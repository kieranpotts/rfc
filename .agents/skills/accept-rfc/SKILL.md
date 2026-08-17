---
name: accept-rfc
description: >-
  Accept a proposed RFC. Use this skill when the user says something like
  "accept this RFC", "approve this RFC", "mark this RFC as accepted",
  "accept RFC", "accept the RFC for <topic>", or otherwise wants to advance a
  proposal to accepted. Do not use this skill to merge an RFC or to assign it
  a number.
compatibility: >-
  requires Read, Edit, Glob, Bash (git, gh)
license: CC0-1.0
---

# Accept RFC

Transition an RFC from `PROPOSED` to `ACCEPTED`: verify the approval gates,
record the decision in the document, and swap the pull request's lifecycle
label to `#accepted`. The RFC is now a settled decision, but its pull request
stays open until the tooling and infrastructure it calls for are in place.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Target — REQUIRED.** The RFC to accept. Infer it from the checked-out
  branch (`latest/rfc/<slug>`). If on `latest/main`, use the user's description,
  or list the open `#proposed` pull requests and ask the user to choose.

- **Decision date — OPTIONAL.** The date the approval was given. Assume today
  if the user does not say otherwise.

## Success criteria

- The document's `Status` field MUST be `ACCEPTED`, `Last updated` MUST be
  today's date, and `Decided by` and `Decision date` MUST be filled in.

- The pull request MUST carry `#accepted` alongside its category label, and
  MUST NOT carry `#proposed`.

- The document change MUST be committed and pushed to the pull request's
  branch.

- The pull request MUST remain open and unmerged, and the discussion thread
  MUST remain open — both stay open through the implementation phase.

- No RFC number MUST have been assigned, and `rfc/INDEX.md` MUST be
  unchanged. Numbering happens at merge, not at acceptance.

## Instructions

1.  Identify the RFC and confirm it is `PROPOSED`.

    Infer the target from the checked-out branch (`latest/rfc/<slug>`). If on
    `latest/main`, use the user's description to infer the target if they gave one;
    otherwise list the open `#proposed` pull requests and ask the user to
    choose:

    ```sh
    gh pr list --label "#proposed" --json number,title,headRefName
    ```

    Check out the branch, then resolve the document by globbing
    `rfc/*/<slug>/README.md` — the category directory is not recoverable from
    the slug alone. Read it, and check its `Status` field is `PROPOSED` and
    the pull request carries `#proposed` and is not a draft:

    ```sh
    gh pr view <number> --json labels,isDraft
    ```

2.  Verify the rules.

    Read the document in full and check each rule below. Report any failure
    and stop without changing anything.

3.  Update the document.

    - Set the `Status` field to `ACCEPTED` and `Last updated` to today's
      date.

    - Fill in `Decided by` and `Decision date`.

    - Confirm `PR` is set, and that any `Implementation trackers` that exist
      are linked.

    Do not assign a number or touch `rfc/INDEX.md` — that happens when the
    pull request is merged, at implementation.

4.  Switch the lifecycle label.

    ```sh
    gh pr edit <number> --add-label "#accepted" --remove-label "#proposed"
    ```

    Leave the category label in place, eg. `ARCHITECTURE`. Leave the pull
    request open, and leave the discussion thread open too — it stays open
    through implementation and is closed only when the pull request merges.

5.  Commit and push.

    Push as well as commit. The pull request stays open through
    implementation, so stakeholders read the RFC's status from the remote —
    an unpushed commit leaves the pull request showing `PROPOSED` after the
    decision was taken.

    ```sh
    git commit -am "update: <short lowercase rfc description>"
    git push
    ```

6.  Queue the implementation.

    Remind the user that the decision now needs to be carried out — the
    tooling and infrastructure it calls for must be built and put in place,
    tracked by issues linked from the document's `Implementation trackers`
    section. The pull request stays open through this phase, and the document
    MAY continue to evolve in response to implementation feedback, with
    feedback continuing on the still-open discussion thread.

## Rules

- You MUST NOT accept an RFC that is not currently `PROPOSED`.

  Never accept a draft, and never move an RFC backwards.

- Stakeholder review MUST have concluded, with feedback gathered from all the
  relevant technical stakeholders.

- The main points of contention MUST be resolved, and the proposed solution
  MUST have stabilized.

- A final-comment period MUST have elapsed with no material change to the
  RFC.

  This is what makes the decision safe to settle: a proposal still moving is
  a proposal still under review.

- Every RFC listed under `Depends on` MUST itself be accepted.

  A decision that rests on an undecided one is not settled.

- You MUST NOT merge the pull request as part of acceptance.

  The pull request stays open until the tooling and infrastructure are in
  place. The merge and the number assignment both happen at implementation.

- You MUST push the status change.

  The pull request remains open through implementation and is what
  stakeholders read. A commit left unpushed leaves the remote showing the
  pre-decision status.

- While the pull request is open, the document MAY continue to evolve.

  Acceptance does not freeze the document. Implementation feedback may be
  reconciled back into it right up to the merge. Only once merged does the
  record become immutable but for its `Status` field, `Last updated` date,
  cross-references, and implementation trackers.
