---
name: reject-rfc
description: >-
  Reject a proposed RFC. Use this skill when the user says "reject this
  RFC", "the RFC was not accepted", "the RFC was not approved", "reject RFC",
  "reject <topic>", or advances a proposal to rejected.
compatibility: requires Read, Edit, Bash (git/gh)
license: CC0-1.0
---

# Reject RFC

Use this skill to transition an RFC from `PROPOSED` to `REJECTED`. A
rejected RFC is not discarded — its document is merged into `main` and
preserved permanently in `rfc/` as the record of the decision and its
rationale, so the same ground is not needlessly covered again later.

## Parameters

Determine the following information from the surrounding context and
environment, if possible.

- **Target — REQUIRED.** Infer the RFC from the checked-out branch
  (`rfc/<slug>`). If on `main`, use the user's description, or list the open
  `#proposed` pull requests and ask the user to choose.

- **Explicit confirmation that the decision is to reject — REQUIRED.**

## Success criteria

<!-- The RFC document updated to `Status: REJECTED`, the PR carrying `#rejected`
and squash-merged into `main`, its discussion thread closed, and a new
numbered row appended to `rfc/INDEX.md`. -->

- `Status` MUST be `REJECTED` and `Last updated` MUST be today's date.

- The PR MUST carry `#rejected` (and its category label).

- The associated discussion thread MUST be closed.

- The user MUST have explicitly confirmed the rejection before any changes
  were made.

- After merge, an `rfc/INDEX.md` entry MUST be added on `main`, with the next
  sequential number.

## Instructions

1.  Confirm the RFC and the decision.

    Infer the target from the current checked-out branch (`rfc/<slug>`). If
    on `main`, use the user's description to infer the target RFC if they
    gave one; otherwise list the open `#proposed` pull requests and ask the
    user to choose:

    ```sh
    gh pr list --label "#proposed" --json number,title,headRefName
    ```

    Identify the document and PR. Confirm with the user that review is
    concluded and the decision is to reject.

2.  Verify the rules.

    Report any unmet rule and stop.

3.  Update the document.

    - Set `Status` to `REJECTED`.
    - Update `Last updated` to today's date.
    - Set `Decision date` to the date the rejection was decided.

    Do not alter any other field as part of this change — the document's
    substance is immutable from this point.

4.  Switch the state label.

    ```sh
    gh pr edit <number> --add-label "#rejected" --remove-label "#proposed"
    ```

5.  Commit and push.

    The push is mandatory: the merge in the next step lands the *remote*
    branch, so an unpushed commit would leave `Status: REJECTED` behind.

    ```sh
    git commit -am "reject: <short lowercase rfc description>"
    git push
    ```

6.  Merge the pull request.

    Confirm with the user that the PR is ready to merge into `main` — do
    not merge without explicit instruction. Once confirmed, squash-merge it
    with the message `rfc: <short lowercase rfc description> - REJECTED`, and
    delete the source branch on the upstream repository:

    ```sh
    gh pr merge <number> --squash --subject "rfc: <short lowercase rfc description> - REJECTED" --delete-branch
    ```

7.  Delete the branch, if it was not deleted automatically.

    In case the branch was not automatically deleted from the upstream
    repository, delete it directly:

    ```sh
    git push origin --delete rfc/<slug>
    ```

8.  Close the associated discussion thread.

    The RFC has merged, so its discussion is now closed. Find the discussion
    linked in the RFC's `Discussion thread` field, look up its node ID, and
    close it as resolved — `gh` has no native discussion command, so use the
    GraphQL API:

    ```gh
    gh api graphql -f query='
      query($owner:String!, $name:String!, $number:Int!) {
        repository(owner:$owner, name:$name) { discussion(number:$number) { id } }
      }' -F owner=<owner> -F name=<repo> -F number=<discussionNumber>

    gh api graphql -f query='
      mutation($id:ID!) {
        closeDiscussion(input:{discussionId:$id, reason:RESOLVED}) { discussion { closed } }
      }' -F id=<discussionId>
    ```

9.  After merge, assign the number.

    The RFC number is assigned only after merge. On `main`, find the highest
    number in [the RFC index](../../../rfc/INDEX.md), increment by one, and
    zero-pad to four digits. Add a row for this RFC — its number, title,
    category, `REJECTED` status, the RFC's `Decision date` (the rejection
    date), and a link to its directory (`rfc/<category>/<slug>/`).

    Commit this directly to `main`, and push:

    ```sh
    git commit -am "chore: assign next rfc number"
    git push
    ```

## Rules

- You MUST NOT delete the RFC document.

  Rejected RFCs are permanently archived as the record of the decision and
  its rationale.

- Stakeholder review MUST have concluded.

  Decision is to reject. Do not proceed until this is explicit.

- The document MUST be a complete record.

  `Motivation`, `Proposed state`, `Alternatives`, and `Trade-offs and risks`
  are substantive. The document will be permanently archived as the record of
  this decision, so its rationale must stand on its own.

- You MUST NOT change RFC document fields other than `Status`, `Last
  updated`, cross-references, and implementation trackers once rejected.

  Once `REJECTED`, only the `Status` field, `Last updated` date,
  cross-references to related RFCs, and implementation trackers may change.
  To revisit the decision, open a new RFC that supersedes this one.

- You MUST push before merging.

  `gh pr merge` merges what is on the remote. A status change committed
  locally but not pushed is silently dropped from `main`, leaving the merged
  RFC still reading `PROPOSED`.

- You MUST NOT merge without explicit instruction from the user.

  Confirm with the user that the PR is ready to merge before running the
  merge command.
