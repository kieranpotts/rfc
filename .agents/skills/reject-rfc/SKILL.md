---
name: reject-rfc
description: Reject a proposed RFC. Use this skill when the user says "reject this RFC", "the RFC was not accepted", "the RFC was not approved", or advances a proposal to rejected.
license: MIT
metadata:
  interactive: yes
---

# `/reject-rfc`

Use this skill to transition an RFC from `PROPOSED` to `REJECTED`. A rejected RFC is not discarded — its document is merged into `main` and preserved permanently in `rfc/` as the record of the decision and its rationale, so the same ground is not needlessly covered again later.

Do NOT use this skill for any other transition — to accept use [`/accept-rfc`](../accept-rfc/SKILL.md), to mark a built decision implemented use [`/implement-rfc`](../implement-rfc/SKILL.md), and to retire a superseded decision use [`/supersede-rfc`](../supersede-rfc/SKILL.md).

## Transition gates: `PROPOSED` → `REJECTED`

The RFC MUST currently be `PROPOSED`. Confirm _all_ of the following before rejecting. If any is unmet, report it and pause.

-   **Stakeholder review has concluded.**

    Decision is to reject. Do not proceed until this is explicit.

-   **The document is a complete record.**

    `Motivation`, `Proposed state`, `Alternatives`, and `Trade-offs and risks` are substantive. The document will be permanently archived as the record of this decision, so its rationale must stand on its own.

##  Instructions

1.  **Confirm the RFC and the decision.**

    Infer the target from the current checked-out branch (`rfc/<slug>`). If on `main`, use the user's description to infer the target RFC if they gave one; otherwise list the open `#proposed` pull requests and ask the user to choose:

    ```sh
    gh pr list --label "#proposed" --json number,title,headRefName
    ```

    Identify the document and PR. Confirm with the user that review is concluded and the decision is to reject.

2.  **Verify the transition gates.**

    Report any unmet gate and stop.

3.  **Update the document.**

    - Set `Status` to `REJECTED`.
    - Update `Last updated` to today's date.
    - Set `Decision date` to the date the rejection was decided.

    Do not alter any other field as part of this change — the document's substance is immutable from this point.

4.  **Switch the state label.**

    ```sh
    gh pr edit <number> --add-label "#rejected" --remove-label "#proposed"
    ```

5.  **Commit.**

    ```sh
    git commit -am "reject: <short lowercase rfc description>"
    ```

6.  **Merge the pull request.**

    Confirm with the user that the PR is ready to merge into `main` — do not merge without explicit instruction. Once confirmed, squash-merge it with the message `rfc: <short lowercase rfc description> - REJECTED`:

    ```sh
    gh pr merge <number> --squash --subject "rfc: <short lowercase rfc description> - REJECTED"
    ```

7.  **Close the associated discussion thread.**

    The RFC has merged, so its discussion is now closed. Find the discussion linked in the RFC's `Discussion thread` field, look up its node ID, and close it as resolved – `gh` has no native discussion command, so use the GraphQL API:

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

8.  **After merge, assign the number.**

    The RFC number is assigned only after merge. On `main`, find the highest number in [the RFC index](../../../rfc/INDEX.md), increment by one, and zero-pad to four digits. Add a row for this RFC — its number, title, category, `Rejected` status, the RFC's `Decision date` (the rejection date), and a link to its directory (`rfc/<category>/<slug>/`).

    Commit this directly to `main`, and push:

    ```sh
    git commit -am "chore: assign next rfc number"
    git push
    ```

##  Rules

-   **Never delete the RFC document.**

    Rejected RFCs are permanently archived as the record of the decision and its rationale.

-   **Immutable after rejection.**

    Once `REJECTED`, only the `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change. To revisit the decision, open a new RFC that supersedes this one.

-   **Do not merge without instruction.**

## Success criteria

- `Status` is `REJECTED` and `Last updated` is today's date.

- The PR carries `#rejected` (and its category label).

- The associated discussion thread is closed.

- The user has explicitly confirmed the rejection before any changes were made.

- After merge: an `rfc/INDEX.md` entry is added on `main`, with the next sequential number.

## References

- [`AGENTS.md`](../../../AGENTS.md): The full RFC lifecycle, rejection path, and immutability rules.
