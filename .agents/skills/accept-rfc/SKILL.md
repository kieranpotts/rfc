---
name: accept-rfc
description: Accept a proposed RFC. Use this skill when the user says "accept this RFC", "approve this RFC", "mark this RFC as accepted", or advances a proposal to accepted.
license: MIT
---

# Accept RFC

Use this skill to transition an RFC from `PROPOSED` to `ACCEPTED`. Verify the approval gates, update the document, label the PR `#accepted`, close its discussion, and squash-merge it. After merge, assign the RFC's number in the RFC index.

Do NOT use this skill for any other transition — to reject use [`reject-rfc`](../reject-rfc/SKILL.md), to retire a superseded decision use [`supersede-rfc`](../supersede-rfc/SKILL.md), to scaffold a draft PR use [`draft-rfc`](../draft-rfc/SKILL.md), and to forward a draft OR to a proposal use [`propose-rfc`](../propose-rfc/SKILL.md).

## Transition gates: `PROPOSED` → `ACCEPTED`

The RFC MUST currently be `PROPOSED`, denoted by a non-draft PR carrying the `#proposed` label). Confirm _all_ of the following before approving. If any is unmet, report it and pause.

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

    Infer the target from the current checked-out branch (`rfc/<slug>`). If on `main`, if the user described the target RFC, try to infer it from that description. If you can't infer the target RFC, list the open `#proposed` pull requests and ask the user to choose:

    ```sh
    gh pr list --label "#proposed" --json number,title,headRefName
    ```

    Read the document. Check `Status` is `PROPOSED` and the PR carries the `#proposed` label and is not a draft (`gh pr view <number> --json labels,isDraft`).

2.  **Verify the transition rules above.**

    Report any unmet gate and stop.

3.  **Update the document.**

    - Set `Status` to `ACCEPTED` and `Last updated` to today's date.

    - Fill in `Approvers` and `Approval date`.

    - Confirm `PR` is set, and that `Implementation trackers` are linked if any exist.

    Do not assign a number or touch `rfc/INDEX.md` yet — the number is assigned only after merge (step 8).

4.  **Switch the state label.**

    ```sh
    gh pr edit <number> --add-label "#accepted" --remove-label "#proposed"
    ```

    Leave the category label, eg. `ARCHITECTURE`.

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

7.  **Merge the pull request.**

    Confirm with the user that the PR is ready to merge into `main` — do not merge without explicit instruction. Once confirmed, squash-merge it with the message `rfc: <short lowercase rfc description> - ACCEPTED`:

    ```sh
    gh pr merge <number> --squash --subject "rfc: <short lowercase rfc description> - ACCEPTED"
    ```

8.  **After merge, assign the number.**

    The RFC number is assigned only after merge. On `main`, find the highest number in [`rfc/INDEX.md`](../../../rfc/INDEX.md), increment by one, zero-pad to four digits (eg. `0006` → `0007`), and add a row for this newly-accepted RFC — its number, title, category, `Accepted` status, the approval date, and a link to its directory (`rfc/<category>/<slug>/`).

    Commit this directly to `main`, and push:

    ```sh
    git commit -am "chore: assign next rfc number"
    git push
    ```

##  Rules

-   **Accept only from `PROPOSED`.**

    Never accept a draft, and never move backwards.

-   **RFCs are immutable after acceptance.**

    After acceptance, only the `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change.

-   **Do not merge without explicit instruction.**

## Success criteria

- `Status` is `ACCEPTED`, `Last updated` is today's date, and `Approvers` / `Approval date` are filled in.

- The PR carries `#accepted` (and its category label), not `#proposed`.

- The associated discussion thread is closed.

- After merge: an `rfc/INDEX.md` entry is added on `main`, with the next sequential number.

## References

- [`AGENTS.md`](../../../AGENTS.md): The full RFC lifecycle and immutability rules.

- [`reject-rfc`](../reject-rfc/SKILL.md) / [`supersede-rfc`](../supersede-rfc/SKILL.md): The other decision transitions.
