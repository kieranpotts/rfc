---
name: complete-rfc
description: >-
  Mark an accepted RFC as implemented once its tooling and infrastructure
  are in place. Use this skill when the user says something like
  "complete RFC", "implement this RFC", "this RFC is implemented",
  "the tooling is in place", "the infrastructure is built", "implement RFC",
  or "<topic> has been implemented". Do not use this skill to carry out the
  implementation work itself.
compatibility: >-
  requires Read, Edit, Glob, Bash (git, gh)
license: CC0-1.0
---

# Complete RFC

Transition an RFC from `ACCEPTED` to `IMPLEMENTED`, once all the tooling and
infrastructure the decision calls for are in place. This is the point at which
the RFC's pull request is squash-merged into `main` and the RFC is assigned its
number in the index. Do not build the tooling or infrastructure yourself.

## Parameters

Determine the following information from the surrounding context and
environment, if possible. If you're uncertain about the required parameters,
prompt the user for clarification.

- **Target — REQUIRED.** The RFC to complete. Infer it from the checked-out
  branch (`rfc/<slug>`). If on `main`, use the user's description, or list the
  open `#accepted` pull requests and ask the user to choose.

## Success criteria

- The document's `Status` field MUST be `IMPLEMENTED` and `Last updated` MUST
  be today's date.

- The pull request MUST carry `#implemented` alongside its category label, and
  MUST NOT carry `#accepted`.

- The pull request MUST be squash-merged into `main` with the message
  `update: <short lowercase rfc description> - IMPLEMENTED`, and its branch
  deleted upstream.

- The discussion thread MUST be closed as resolved.

- A row for the RFC MUST have been added to `rfc/INDEX.md` on `main`, with
  the next sequential number and `IMPLEMENTED` status.

- No repository outside this one MUST have been touched. The tooling and
  infrastructure are built elsewhere, and this skill only records that they
  are in place.

## Instructions

1.  Identify the RFC and confirm it is `ACCEPTED`.

    Infer the target from the checked-out branch (`rfc/<slug>`). If on
    `main`, use the user's description to infer the target if they gave one;
    otherwise list the open `#accepted` pull requests and ask the user to
    choose:

    ```sh
    gh pr list --label "#accepted" --json number,title,headRefName
    ```

    Check out the branch, then resolve the document by globbing
    `rfc/*/<slug>/README.md` — the category directory is not recoverable from
    the slug alone. Read it, and check its `Status` field is `ACCEPTED` and
    the pull request carries `#accepted`:

    ```sh
    gh pr view <number> --json labels
    ```

2.  Verify the rules.

    Report any failure and stop without changing anything.

3.  Update the document.

    - Set the `Status` field to `IMPLEMENTED` and `Last updated` to today's
      date.
    - Confirm `Implementation trackers` are linked.
    - Reconcile any drift discovered during implementation back into the
      document, so the merged record describes the decision as it was
      actually realized. This is the last point at which that is permitted.

4.  Switch the lifecycle label.

    ```sh
    gh pr edit <number> --add-label "#implemented" --remove-label "#accepted"
    ```

    Leave the category label in place, eg. `TOOLING`.

5.  Commit and push.

    The push is mandatory: the merge in the next step lands the *remote*
    branch, so an unpushed commit would leave `Status: IMPLEMENTED` behind.

    ```sh
    git commit -am "update: <short lowercase rfc description>"
    git push
    ```

6.  Merge the pull request.

    Confirm with the user that the pull request is ready to merge into `main`
    — do not merge without explicit instruction. Once confirmed, squash-merge
    it and delete the source branch upstream:

    ```sh
    gh pr merge <number> --squash --subject "update: <short lowercase rfc description> - IMPLEMENTED" --delete-branch
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
    its number, title, category, `IMPLEMENTED` status, its `Decision date`
    (the approval date), and a link to its directory
    (`rfc/<category>/<slug>/`).

    Commit this directly to `main`, and push:

    ```sh
    git checkout main
    git pull --rebase
    git commit -am "chore: assign rfc <number>"
    git push
    ```

10. Report what you did, naming the number the RFC was assigned. An
    implemented RFC stays in effect until a later RFC replaces its decision.

## Rules

- You MUST NOT complete an RFC that is not currently `ACCEPTED`.

  Never merge a draft, a proposal still under review, or a rejected RFC
  through this route.

- The tooling and infrastructure MUST genuinely be in place.

  Everything the decision calls for — tools, automation, infrastructure,
  configuration, conventions — has actually been built and put into effect,
  not merely planned. That is what keeps the archive honest: `IMPLEMENTED`
  has to mean the reader can go and find the thing.

- Every RFC listed under `Depends on` MUST itself be implemented.

  A decision cannot be in effect while a decision it rests on is not.

- The RFC document MUST reflect the decision as carried out.

  Any drift discovered during implementation is reconciled back into the
  document before the merge.

- You MUST push before merging.

  `gh pr merge` merges what is on the remote. A status change committed
  locally but not pushed is silently dropped from `main`, leaving the merged
  RFC still reading `ACCEPTED`.

- You MUST NOT merge without explicit instruction from the user.

  Confirm the pull request is ready to merge before running the merge
  command.

- Once merged, you MUST NOT change any document field other than `Status`,
  `Last updated`, cross-references, and implementation trackers.

  The merged record is immutable in every other respect. To change a decision
  already in effect, draft a new RFC that replaces it.

## Edge cases

- The direct push to `main` in step 9 is rejected by branch protection.

  That step is a deterministic, mechanical edit — the next sequential
  number — with nothing for a human reviewer to weigh in on, which is why
  it pushes directly rather than opening a pull request. Where `main` is
  protected against direct pushes even so, open a small pull request
  carrying the same commit instead, merge it immediately, and tell the
  user this fallback was needed, since it means `main` is protected in a
  way this skill did not expect going in.
