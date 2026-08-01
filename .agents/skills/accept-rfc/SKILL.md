---
name: accept-rfc
description: >-
  Accept a proposed RFC. Use this skill when the user says something like
  "accept this RFC", "approve this RFC", "mark this RFC as accepted",
  "accept RFC", "accept the RFC for <topic>", or otherwise wants to advance a
  proposal to accepted.
license: MIT
metadata:
  interactive: yes
  preferred_model: prose-writing
---

# Accept RFC

Use this skill to transition an RFC from `PROPOSED` to `ACCEPTED`: verify the
approval gates, update the document, and label the PR `#accepted`. The RFC is
now a settled decision, but its pull request stays open until the tooling and
infrastructure it calls for are in place. The discussion thread stays open
through implementation and is closed only when the PR is merged.

## Parameters

Determine the following information from the surrounding context and
environment, if possible.

- **Target — REQUIRED.** Infer the RFC from the checked-out branch
  (`rfc/<slug>`). If on `main`, use the user's description, or list the open
  `#proposed` pull requests and ask the user to choose.

## Success criteria

You will achieve the following outcomes:

<!-- The RFC document updated to `Status: ACCEPTED` with `Decided by` and
`Decision date` filled in, the PR carrying `#accepted` and left open. -->

- `Status` is `ACCEPTED`, `Last updated` is today's date, and `Decided by` /
  `Decision date` are filled in.

- The PR carries `#accepted` (and its category label), not `#proposed`, and
  remains open.

- The associated discussion thread remains open.

  It is closed when the PR is merged at implementation.

- No number has been assigned.

  That waits for implementation.

## Instructions

1.  Identify the RFC and confirm it is `PROPOSED`.

    Infer the target from the current checked-out branch (`rfc/<slug>`). If
    on `main`, use the user's description to infer the target RFC if they
    gave one; otherwise list the open `#proposed` pull requests and ask the
    user to choose:

    ```sh
    gh pr list --label "#proposed" --json number,title,headRefName
    ```

    Read the document. Check `Status` is `PROPOSED` and the PR carries the
    `#proposed` label and is not a draft (`gh pr view <number> --json
    labels,isDraft`).

2.  Verify the rules.

    Report any unmet rule and stop.

3.  Update the document.

    - Set `Status` to `ACCEPTED` and `Last updated` to today's date.

    - Fill in `Decided by` and `Decision date` (the approval date).

    - Confirm `PR` is set, and that `Implementation trackers` are linked if
      any exist.

    Do not assign a number or touch `rfc/INDEX.md` — that happens at merge,
    in [`/complete-rfc`](../complete-rfc/SKILL.md).

4.  Switch the state label.

    ```sh
    gh pr edit <number> --add-label "#accepted" --remove-label "#proposed"
    ```

    Leave the category label, eg. `ARCHITECTURE`. Keep the PR open — do not
    merge. Leave the discussion thread open too; it stays open through
    implementation and is closed only when the PR is merged.

5.  Commit.

    ```sh
    git commit -am "accept: <short lowercase rfc description>"
    ```

    Keep the PR open — do not merge, and do not assign a number. Both happen
    at implementation.

6.  Queue the implementation.

    Remind the user that the decision now needs to be carried out — the
    tooling and infrastructure it calls for must be built and put in place.
    The PR stays open through this phase; the document MAY continue to evolve
    in response to implementation feedback, with feedback continuing on the
    still-open discussion thread. When the tooling and infrastructure are in
    place, run [`/complete-rfc`](../complete-rfc/SKILL.md).

## Rules

- You MUST NOT accept an RFC that is not currently `PROPOSED`.

  Never accept a draft, and never move backwards.

- Stakeholder review MUST have concluded.

  Feedback gathered from all relevant stakeholders.

- The main points of contention MUST be resolved.

  The proposed solution has stabilized.

- A final-comment period MUST have elapsed.

  There have been no material changes to the RFC in this period.

- Blocking decisions MUST be resolved.

  Every RFC listed under `Depends on` is itself accepted.

- You MUST NOT merge the pull request as part of acceptance.

  The PR stays open until the tooling and infrastructure are in place. The
  merge and the number assignment happen at implementation, not acceptance.

- You MUST NOT change RFC document fields other than `Status`, `Last
  updated`, cross-references, and implementation trackers once merged.

  While the PR is open — including through implementation — the document MAY
  still evolve. Once merged at `#implemented`, only the `Status` field, `Last
  updated` date, cross-references to related RFCs, and implementation
  trackers may change.
