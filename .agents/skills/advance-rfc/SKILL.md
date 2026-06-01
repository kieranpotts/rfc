---
name: advance-rfc
description: Transition an RFC from its current lifecycle state to the next permitted state, verifying that all checklist gates are satisfied first. Use when the user wants to move an RFC to the next state, says "advance this RFC", "mark this as proposed/accepted/superseded", or asks to apply a lifecycle label to an RFC PR.
license: MIT
---

# Advance RFC

Use this skill to move an RFC through its lifecycle state machine. It verifies that the gates for the target state are met, updates the RFC document's `Status` field and `Last updated` date, and applies the matching GitHub label to the PR.

Do NOT use this skill to scaffold a new RFC (use [`draft-rfc`](../draft-rfc/SKILL.md)) or to audit an RFC's content (use [`audit-rfc`](../audit-rfc/SKILL.md)). For the rejection path specifically, use [`reject-rfc`](../reject-rfc/SKILL.md). Do NOT move an RFC backwards or skip states — those transitions are not permitted.

## Instructions

1.  **Identify the RFC and its current state.**

    If not already open, read the RFC document in `rfcs/`. Check the `Status` field and confirm it matches the current `#label` on the PR (run `gh pr view <number> --json labels` if needed).

2.  **Determine the target state.**

    The permitted transitions are:

    | From | To | Key gate |
    | --- | --- | --- |
    | `DRAFT` | `PROPOSED` | Document complete; originating issue closed |
    | `PROPOSED` | `ACCEPTED` | Stakeholder review concluded; ID assigned |
    | `PROPOSED` | `REJECTED` | Stakeholder review concluded (use [`reject-rfc`](../reject-rfc/SKILL.md)) |
    | `ACCEPTED` | `SUPERSEDED` | A later RFC has replaced this decision |

    If the user requests an unlisted transition (eg. `PROPOSED` back to `DRAFT`), refuse and explain why. For `PROPOSED → REJECTED`, hand off to the [`reject-rfc`](../reject-rfc/SKILL.md) skill.

3.  **Verify the gates for the target state.**

    Run [`audit-rfc`](../audit-rfc/SKILL.md) against the RFC and confirm the relevant checklist gates in `.github/PULL_REQUEST_TEMPLATE.md` are satisfied. Report any unmet gates to the user and pause for direction before proceeding.

4.  **For `PROPOSED → ACCEPTED`: assign the sequential ID.**

    Find the highest existing numeric ID in `rfcs/` (eg. `0003-foo.md` → `0003`). Increment by one, zero-padded to four digits. Rename the file:

    ```sh
    git mv rfcs/<slug>.md rfcs/<NNNN>-<slug>.md
    ```

    Update the `PR` field in the document if it is not yet set.

5.  **Update the RFC document.**

    - Update `Status` to the new state and `Last updated` to today's date.
    - For `ACCEPTED`: Fill in `Approvers` and `Approval date`, and confirm that `Implementation trackers` links are present.
    - For `SUPERSEDED`: confirm the `Superseded by` field links the later RFC.

    Once an RFC is `ACCEPTED`, only its `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change on the subsequent transition to `SUPERSEDED` — the rest of the document is immutable.

6.  **Apply the GitHub label.**

    ```sh
    gh pr edit <number> --add-label "#<state>" --remove-label "#<previous-state>"
    ```

    Use the lowercase `#`-prefixed label names: `#draft`, `#proposed`, `#accepted`, `#rejected`, `#superseded`. This swaps only the lifecycle label; leave the PR's category label (`ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`) in place.

7.  **Commit.**

    Stage and commit the updated document (and any file rename). Use the commit message convention from the `commit` skill if available, otherwise `chore: advance RFC to <state>`.

## Rules

-   **Only maintainers may advance an RFC's state.**

    If there is any indication the current user does not have that role, note it and ask for confirmation before proceeding.

-   **Never move backwards or skip states.**

    The state machine is strictly forward-only. If a correction is needed, open a new RFC that supersedes the original.

-   **Once `ACCEPTED` or `REJECTED`, the document is immutable.**

    After those states are reached, only its `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change (along with the matching GitHub label on the PR). Do not edit any other part of the document.

-   **Gate verification is mandatory.**

    Do not advance state without running [`audit-rfc`](../audit-rfc/SKILL.md) first. An unchecked gate is a process violation, not a minor omission.

## Success criteria

-   **The RFC document's `Status` matches the new state.**

-   **`Last updated` is set to today's date.**

-   **The GitHub PR label is updated** to the matching `#<state>` label.

-   **For `#accepted`: the file has been renamed** to `NNNN-<slug>.md` with the correct sequential ID.

-   **No prohibited transition was performed.**

## References

- [AGENTS.md](../../../AGENTS.md): State machine, permitted transitions, and immutability rules.

- [PR checklist](../../../.github/PULL_REQUEST_TEMPLATE.md): The gates that must be satisfied before each transition.

- [`audit-rfc`](../audit-rfc/SKILL.md): Run this skill before advancing to verify gates.

- [`reject-rfc`](../reject-rfc/SKILL.md): Dedicated skill for the rejection path.
