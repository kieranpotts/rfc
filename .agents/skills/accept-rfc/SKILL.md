---
name: accept-rfc
description: Accept a proposed RFC. Use this skill when the user says "accept this RFC", "approve this RFC", "mark this RFC as accepted", or otherwise wants to advance a proposal to accepted.
license: MIT
---

# Accept RFC

Use this skill to transition an RFC from `PROPOSED` to `ACCEPTED`: verify the approval gates, update the document, label the PR `#accepted`, and close its discussion thread. The RFC is now a settled decision, but its pull request stays open until the tooling and infrastructure it calls for are in place.

Do NOT use this skill for any other transition — to mark a built decision implemented use [`implement-rfc`](../implement-rfc/SKILL.md), to reject use [`reject-rfc`](../reject-rfc/SKILL.md), to retire a superseded decision use [`supersede-rfc`](../supersede-rfc/SKILL.md), to scaffold a draft PR use [`draft-rfc`](../draft-rfc/SKILL.md), and to forward a draft to a proposal use [`propose-rfc`](../propose-rfc/SKILL.md).

## Transition gates: `PROPOSED` → `ACCEPTED`

The RFC MUST currently be `PROPOSED`, denoted by a non-draft PR carrying the `#proposed` label. Confirm _all_ of the following before approving. If any is unmet, report it and pause.

-   **Stakeholder review has concluded.**

    Feedback gathered from all relevant stakeholders.

-   **The main points of contention are resolved.**

    The proposed solution has stabilized.

-   **A final-comment period has elapsed.**

    There have been no material changes to the RFC in this period.

-   **Blocking decisions are resolved.**

    Every RFC listed under `Depends on` is itself accepted.

##  Instructions

1.  **Identify the RFC and confirm it is `PROPOSED`.**

    Infer the target from the current checked-out branch (`rfc/<slug>`). If on `main`, use the user's description to infer the target RFC if they gave one; otherwise list the open `#proposed` pull requests and ask the user to choose:

    ```sh
    gh pr list --label "#proposed" --json number,title,headRefName
    ```

    Read the document. Check `Status` is `PROPOSED` and the PR carries the `#proposed` label and is not a draft (`gh pr view <number> --json labels,isDraft`).

2.  **Verify the transition gates.**

    Report any unmet gate and stop.

3.  **Update the document.**

    - Set `Status` to `ACCEPTED` and `Last updated` to today's date.

    - Fill in `Approvers` and `Approval date`.

    - Confirm `PR` is set, and that `Implementation trackers` are linked if any exist.

    Do not assign a number or touch `rfc/INDEX.md` — that happens at merge, in [`implement-rfc`](../implement-rfc/SKILL.md).

4.  **Switch the state label.**

    ```sh
    gh pr edit <number> --add-label "#accepted" --remove-label "#proposed"
    ```

    Leave the category label, eg. `ARCHITECTURE`. Keep the PR **open** — do not merge.

5.  **Close the associated discussion thread.**

    Find the discussion linked in the RFC's `Discussion thread` field, look up its node ID, and close it as resolved – `gh` has no native discussion command, so use the GraphQL API:

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

6.  **Commit.**

    ```sh
    git commit -am "accept: <short lowercase rfc description>"
    ```

    Keep the PR **open** — do not merge, and do not assign a number. Both happen at implementation.

7.  **Queue the implementation.**

    Remind the user that the decision now needs to be carried out — the tooling and infrastructure it calls for must be built and put in place. The PR stays open through this phase; the document MAY continue to evolve in response to implementation feedback. When the tooling and infrastructure are in place, run [`implement-rfc`](../implement-rfc/SKILL.md).

##  Rules

-   **Accept only from `PROPOSED`.**

    Never accept a draft, and never move backwards.

-   **Acceptance is a decision, not a merge.**

    The PR stays open until the tooling and infrastructure are in place. The merge and the number assignment happen at implementation, not acceptance.

-   **RFCs are immutable after merge.**

    While the PR is open — including through implementation — the document MAY still evolve. Once merged at `#implemented`, only the `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change.

## Success criteria

- `Status` is `ACCEPTED`, `Last updated` is today's date, and `Approvers` / `Approval date` are filled in.

- The PR carries `#accepted` (and its category label), not `#proposed`, and remains open.

- The associated discussion thread is closed.

- No number has been assigned — that waits for implementation.

## References

- [`AGENTS.md`](../../../AGENTS.md): The full RFC lifecycle and immutability rules.
