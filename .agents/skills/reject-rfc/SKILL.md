---
name: reject-rfc
description: Handle the rejection path for an RFC: assign its sequential ID, set its status to rejected, and prepare the pull request for merge so the decision is preserved permanently. Use when the user says "reject this RFC", "the RFC was not approved", or when advancing an RFC from proposed to rejected.
license: MIT
---

# Reject RFC

Use this skill to handle the rejection path for an RFC. A rejected RFC is not discarded — its document is merged into `main` and preserved permanently in `rfcs/` as the record of the decision and its rationale, so the same ground is not needlessly re-trodden later.

Because this repository is an append-only archive of decisions (it holds no "current state" that a rejected RFC would have changed), rejection is straightforward — there is nothing to revert. The RFC simply lands as the record.

Do NOT use this skill to advance an RFC to any state other than `REJECTED`. For all other transitions, use [`advance-rfc`](../advance-rfc/SKILL.md). For auditing, use [`audit-rfc`](../audit-rfc/SKILL.md).

## Instructions

1.  **Confirm the RFC and the decision.**

    Identify the RFC document and PR. Confirm with the user that the stakeholder review is concluded and the decision is to reject. Do not proceed until this is explicit.

2.  **Run a pre-rejection audit.**

    Run [`audit-rfc`](../audit-rfc/SKILL.md) to verify the document is complete. The `Motivation`, `Proposed change`, `Alternatives`, and `Trade-offs and risks` sections should be substantive, since the document will be permanently archived as the record of this decision.

3.  **Assign the sequential ID.**

    Find the highest existing numeric ID in `rfcs/` and increment by one, zero-padded to four digits. Rename the file:

    ```sh
    git mv rfcs/<slug>.md rfcs/<NNNN>-<slug>.md
    ```

    Rejected RFCs are numbered in the same sequence as accepted ones.

4.  **Update the RFC document.**

    - Set `Status` to `REJECTED`.
    - Update `Last updated` to today's date.
    - Do not alter any other field as part of this change — the document's substance is immutable from this point.

5.  **Apply the GitHub label.**

    ```sh
    gh pr edit <number> --add-label "#rejected" --remove-label "#proposed"
    ```

    This swaps only the lifecycle label; leave the PR's category label (`ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`) in place.

6.  **Commit.**

    ```sh
    git add rfcs/
    git commit -m "chore: reject RFC <slug>"
    ```

7.  **Confirm the PR is ready to merge.**

    Confirm with the user that the PR is ready to merge into `main`. Do not merge without explicit instruction.

## Rules

-   **Never delete the RFC document.**

    Rejected RFCs are permanently archived in `rfcs/`. The document is the record of the decision and its rationale.

-   **The document is immutable after being rejected.**

    Once the RFC reaches the `REJECTED` status, no further edits are permitted except to update its `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers. To revisit the decision, open a new RFC that supersedes this one using the `Supersedes` field.

-   **Do not merge without instruction.**

    Prepare the PR and confirm it is ready, but wait for explicit confirmation before merging.

## Success criteria

-   **The file has been renamed** to `NNNN-<slug>.md` with the correct sequential ID.

-   **The RFC document's `Status` is `REJECTED`** and `Last updated` is today's date.

-   **The GitHub PR label is `#rejected`.**

-   **The user has explicitly confirmed** the rejection decision before any changes were made.

## References

- [AGENTS.md](../../../AGENTS.md): Describes the RFC state machine, rejection path, and immutability rules for agents.

- [PR checklist](../../../.github/PULL_REQUEST_TEMPLATE.md): The rejection gates.

- [`audit-rfc`](../audit-rfc/SKILL.md): Run this skill before rejecting an RFC, to confirm the document is complete.

- [`advance-rfc`](../advance-rfc/SKILL.md): For all other state transitions.
