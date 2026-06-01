---
name: approve-rfc
description: Approve a proposed RFC — record its number in the index, set its status to accepted, label the PR, and prepare it for merge. Use when the user says "approve this RFC", "accept this RFC", "mark this RFC accepted", or advances a proposal to accepted.
license: MIT
---

# Approve RFC

Use this skill to move an RFC from **proposed** to **accepted**: verify the approval gates, record the RFC number in the index, update the document, label the PR `#accepted`, close its discussion, and prepare it for merge.

Do NOT use this skill for any other transition — to reject use [`reject-rfc`](../reject-rfc/SKILL.md), to retire a superseded decision use [`supersede-rfc`](../supersede-rfc/SKILL.md), and to scaffold or propose use [`draft-rfc`](../draft-rfc/SKILL.md) / [`propose-rfc`](../propose-rfc/SKILL.md).

## Transition rules (proposed → accepted)

The RFC MUST currently be `PROPOSED` (a non-draft PR carrying `#proposed`). Confirm **all** of the following before approving. If any is unmet, report it and pause.

-   **Stakeholder review has concluded**, with feedback gathered from all relevant stakeholders.
-   **The main points of contention are resolved** and the proposed solution has stabilized.
-   **A final-comment period has elapsed** (per project convention) with no material change to the document during it.
-   **Blocking decisions are resolved** — every RFC listed under `Depends on` is itself accepted.
-   **Only maintainers may approve.** If there is any indication the current user is not a maintainer, ask for confirmation first.

## Instructions

1.  **Identify the RFC and confirm it is `PROPOSED`.**

    Read the document; check `Status` is `PROPOSED` and the PR carries `#proposed` and is not a draft (`gh pr view <number> --json labels,isDraft`).

2.  **Verify the transition rules above.**

    Report any unmet gate and stop.

3.  **Add the RFC to the index.**

    Find the highest RFC number in [`rfc/INDEX.md`](../../../rfc/INDEX.md), increment by one, and zero-pad to four digits (eg. `0006` → `0007`). Add a row for this RFC — its number, title, category, `Accepted` status, the approval date, and a link to its directory (`rfc/<category>/<slug>/`). The number lives only in the index; the RFC's directory and files are never renamed.

4.  **Update the document.**

    - Set `Status` to `ACCEPTED` and `Last updated` to today's date.
    - Fill in `Approvers` and `Approval date`.
    - Confirm `PR` is set, and that `Implementation trackers` are linked if any exist.

5.  **Apply the label.**

    ```sh
    gh pr edit <number> --add-label "#accepted" --remove-label "#proposed"
    ```

    This swaps only the lifecycle label; leave the category label in place.

6.  **Close the associated discussion thread.**

    A decided RFC's discussion is closed. Find the discussion linked in the RFC's `Discussion thread` field, look up its node ID, and close it as resolved (`gh` has no native discussion command, so use the GraphQL API):

    ```sh
    gh api graphql -f query='
      query($owner:String!, $name:String!, $number:Int!) {
        repository(owner:$owner, name:$name) { discussion(number:$number) { id } }
      }' -F owner=<owner> -F name=<repo> -F number=<discussionNumber>

    gh api graphql -f query='
      mutation($id:ID!) {
        closeDiscussion(input:{discussionId:$id, reason:RESOLVED}) { discussion { closed } }
      }' -F id=<discussionId>
    ```

7.  **Commit.**

    ```sh
    git commit -am "rfc: accept <slug> (RFC <NNNN>)"
    ```

8.  **Prepare for merge.**

    Confirm with the user that the PR is ready to merge into `main`. Do not merge without explicit instruction. An accepted RFC remains in effect until a later RFC supersedes it (see [`supersede-rfc`](../supersede-rfc/SKILL.md)).

## Rules

-   **Only maintainers may approve.** If unsure of the user's role, ask first.

-   **Forward only.** Approve only from `PROPOSED`. Never accept a draft, and never move backwards.

-   **Immutable once accepted.** After acceptance, only the `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change.

-   **Do not merge without instruction.**

## Success criteria

-   **An `rfc/INDEX.md` entry is added** for the RFC, with the next sequential number.

-   **`Status` is `ACCEPTED`**, `Last updated` is today's date, and `Approvers` / `Approval date` are filled in.

-   **The PR carries `#accepted`** (and its category label), not `#proposed`.

-   **The associated discussion thread is closed.**

## References

- [AGENTS.md](../../../AGENTS.md): The full RFC lifecycle and immutability rules.

- [`reject-rfc`](../reject-rfc/SKILL.md) / [`supersede-rfc`](../supersede-rfc/SKILL.md): The other decision transitions.
