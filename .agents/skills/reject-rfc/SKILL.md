---
name: reject-rfc
description: >-
  Reject a proposed RFC. Use this skill when the user says "reject this
  RFC", "the RFC was not accepted", "the RFC was not approved", "reject RFC",
  "reject <topic>", or advances a proposal to rejected. Do not use this skill
  to delete an RFC or to withdraw one that was never proposed.
compatibility: >-
  requires Read, Edit, Glob, Bash (git, gh)
license: CC0-1.0
---

# Reject RFC

Transition an RFC from `PROPOSED` to `REJECTED`. A rejected RFC is not
discarded: its document is merged into `main` and preserved permanently in
`rfc/` as the record of the decision and its rationale, so the same ground is
not needlessly covered again later.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Target — REQUIRED.** The RFC to reject. Infer it from the checked-out
  branch (`rfc/<slug>`). If on `main`, use the user's description, or list the
  open `#proposed` pull requests and ask the user to choose.

- **Explicit confirmation that the decision is to reject — REQUIRED.** Ask
  the user directly. Rejection is irreversible in this lifecycle: reopening
  the question means drafting a fresh RFC.

- **Decision date — OPTIONAL.** The date the rejection was decided. Assume
  today if the user does not say otherwise.

## Success criteria

- The document's `Status` field MUST be `REJECTED`, `Last updated` MUST be
  today's date, and `Decided by` and `Decision date` MUST be filled in.

- The pull request MUST carry `#rejected` alongside its category label, and
  MUST NOT carry `#proposed`.

- The pull request MUST be squash-merged into `main` with the message
  `update: <short lowercase rfc description> - REJECTED`, and its branch
  deleted upstream.

- The discussion thread MUST be closed as resolved.

- A row for the RFC MUST have been added to `rfc/INDEX.md` on `main`, with
  the next sequential number and `REJECTED` status.

- The RFC document MUST NOT have been deleted, and no section of it other
  than the metadata header and `Status` MUST have changed.

## Instructions

1.  Identify the RFC and confirm the decision.

    Infer the target from the checked-out branch (`rfc/<slug>`). If on
    `main`, use the user's description to infer the target if they gave one;
    otherwise list the open `#proposed` pull requests and ask the user to
    choose:

    ```sh
    gh pr list --label "#proposed" --json number,title,headRefName
    ```

    Check out the branch, then resolve the document by globbing
    `rfc/*/<slug>/README.md` — the category directory is not recoverable from
    the slug alone. Read it, check its `Status` field is `PROPOSED`, and
    confirm with the user that review has concluded and the decision is to
    reject.

2.  Verify the rules.

    Report any failure and stop without changing anything.

3.  Update the document.

    - Set the `Status` field to `REJECTED`.
    - Update `Last updated` to today's date.
    - Fill in `Decided by` and `Decision date`.

    Change nothing else — the document's substance is immutable from this
    point, and it is about to become the permanent record of the decision.

4.  Switch the lifecycle label.

    ```sh
    gh pr edit <number> --add-label "#rejected" --remove-label "#proposed"
    ```

    Leave the category label in place, eg. `ARCHITECTURE`.

5.  Commit and push.

    The push is mandatory: the merge in the next step lands the *remote*
    branch, so an unpushed commit would leave `Status: REJECTED` behind.

    ```sh
    git commit -am "update: <short lowercase rfc description>"
    git push
    ```

6.  Merge the pull request.

    Confirm with the user that the pull request is ready to merge into `main`
    — do not merge without explicit instruction. Once confirmed, squash-merge
    it and delete the source branch upstream:

    ```sh
    gh pr merge <number> --squash --subject "update: <short lowercase rfc description> - REJECTED" --delete-branch
    ```

7.  Delete the branch, if it was not deleted automatically.

    ```sh
    git push origin --delete rfc/<slug>
    ```

8.  Close the discussion thread.

    The RFC has merged, so its discussion is now closed. Find the discussion
    linked from the document's `Discussion thread` field, look up its node
    ID, and close it as resolved — `gh` has no native discussion command, so
    use the GraphQL API:

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

9.  After merge, assign the RFC number.

    The number is assigned only after merge. On `main`, find the highest
    number in [the RFC index](../../../rfc/INDEX.md), increment by one, and
    zero-pad to four digits (eg. `0006` → `0007`). Add a row for this RFC —
    its number, title, category, `REJECTED` status, its `Decision date`, and
    a link to its directory (`rfc/<category>/<slug>/`).

    Commit this directly to `main`, and push:

    ```sh
    git checkout main
    git pull --rebase
    git commit -am "chore: assign next rfc number"
    git push
    ```

10. Report what you did, naming the number the RFC was assigned.

## Rules

- You MUST NOT reject an RFC that is not currently `PROPOSED`.

  Only a proposal that has been through stakeholder review can be rejected.
  An RFC still in draft is withdrawn by abandoning its branch, not by
  rejection.

- You MUST NOT delete the RFC document.

  Rejected RFCs are archived permanently as the record of the decision and
  its rationale. Deleting one destroys the institutional memory of a question
  already settled.

- Stakeholder review MUST have concluded, and the user MUST have explicitly
  confirmed that the decision is to reject.

  Do not proceed on an inference. Get the confirmation in words.

- The document MUST be a complete record.

  `Motivation`, `Proposed state`, `Alternatives`, and `Trade-offs and risks`
  are substantive. The document is about to be archived permanently, so its
  rationale has to stand on its own without the discussion thread.

- You MUST push before merging.

  `gh pr merge` merges what is on the remote. A status change committed
  locally but not pushed is silently dropped from `main`, leaving the merged
  RFC still reading `PROPOSED`.

- You MUST NOT merge without explicit instruction from the user.

  Confirm the pull request is ready to merge before running the merge
  command.

- Once merged, you MUST NOT change any document field other than `Status`,
  `Last updated`, cross-references, and implementation trackers.

  To revisit a rejected decision, draft a new RFC rather than editing this
  one.

## Edge cases

- The direct push to `main` in step 9 is rejected by branch protection.

  That step is a deterministic, mechanical edit — the next sequential
  number — with nothing for a human reviewer to weigh in on, which is why
  it pushes directly rather than opening a pull request. Where `main` is
  protected against direct pushes even so, open a small pull request
  carrying the same commit instead, merge it immediately, and tell the
  user this fallback was needed, since it means `main` is protected in a
  way this skill did not expect going in.
