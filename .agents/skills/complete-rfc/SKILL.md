---
name: complete-rfc
description: >-
  Mark an accepted RFC as implemented once its tooling and infrastructure
  are in place. Use this skill when the user says something like
  "complete RFC", "implement this RFC", "this RFC is implemented",
  "the tooling is in place", "the infrastructure is built", "implement RFC",
  or "<topic> has been implemented".
license: CC0-1.0
metadata:
  interactive: yes
  preferred_model: ollama/technical-reasoning
---

# Complete RFC

Use this skill to transition an RFC from `ACCEPTED` to `IMPLEMENTED`, once
all the tooling and infrastructure the decision calls for are in place.
This is the point at which the RFC's pull request is squash-merged into
`main` and the RFC is assigned its number in the
[RFC index](../../../rfc/INDEX.md).

An accepted RFC is a settled decision whose pull request stays open through
the implementation phase.

## Parameters

Determine the following information from the surrounding context and
environment, if possible.

- **Target — REQUIRED.** Infer the RFC from the checked-out branch
  (`rfc/<slug>`). If on `main`, use the user's description, or list the open
  `#accepted` pull requests and ask the user to choose.

## Success criteria

You will achieve the following outcomes:

<!-- The RFC document updated to `Status: IMPLEMENTED`, the PR carrying
`#implemented` and squash-merged into `main`, its discussion thread closed,
and a new numbered row appended to `rfc/INDEX.md`. -->

- `Status` is `IMPLEMENTED` and `Last updated` is today's date.

- The PR carries `#implemented` (and its category label), not `#accepted`.

- The RFC document is squash-merged into `main`.

- The associated discussion thread is closed.

- After merge: an `rfc/INDEX.md` entry is added on `main`, with the next
  sequential number and `IMPLEMENTED` status.

## Instructions

1.  Identify the RFC and confirm it is `ACCEPTED`.

    Infer the target from the current checked-out branch (`rfc/<slug>`). If
    on `main`, use the user's description to infer the target RFC if they
    gave one, otherwise list the open `#accepted` pull requests and ask the
    user to choose:

    ```sh
    gh pr list --label "#accepted" --json number,title,headRefName
    ```

    Read the document. Check `Status` is `ACCEPTED` and the PR carries
    `#accepted` (`gh pr view <number> --json labels`).

2.  Verify the rules.

    Report any unmet rule and stop.

3.  Update the document.

    - Set `Status` to `IMPLEMENTED` and `Last updated` to today's date.
    - Confirm `Implementation trackers` are linked.

4.  Switch the state label.

    ```sh
    gh pr edit <number> --add-label "#implemented" --remove-label "#accepted"
    ```

    This swaps only the lifecycle label. Leave the category label, eg.
    `TOOLING`, in place.

5.  Commit and push.

    The push is mandatory: the merge in the next step lands the *remote*
    branch, so an unpushed commit would leave `Status: IMPLEMENTED` behind.

    ```sh
    git commit -am "implement: <short lowercase rfc description>"
    git push
    ```

6.  Merge the pull request.

    The RFC document is now ready to land on `main`. Confirm with the user
    that the PR is ready to merge — do not merge without explicit
    instruction. Once confirmed, squash-merge it with the message `rfc: <short
    lowercase rfc description> - IMPLEMENTED`, and delete the source branch on
    the upstream repository:

    ```sh
    gh pr merge <number> --squash --subject "rfc: <short lowercase rfc description> - IMPLEMENTED" --delete-branch
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
    number in [RFC index](../../../rfc/INDEX.md), increment by one, zero-pad
    to four digits (eg. `0006` → `0007`), and add a row for this RFC — its
    number, title, category, `IMPLEMENTED` status, the RFC's `Decision date`
    (its approval date), and a link to its directory
    (`rfc/<category>/<slug>/`).

    Commit this directly to `main`, and push:

    ```sh
    git commit -am "chore: assign rfc <number>"
    git push
    ```

    An implemented RFC stays in effect until a later RFC supersedes it.

## Rules

- You MUST NOT implement an RFC that is not currently `ACCEPTED`.

  Never implement a draft, proposed, or rejected RFC.

- The tooling and infrastructure MUST be in place.

  Everything the decision calls for — the tools, automation,
  infrastructure, configuration, or conventions — has actually been built
  and put into effect, not merely planned.

- The RFC document MUST reflect the decision as carried out.

  Any drift discovered during implementation has been reconciled back into
  the document, so the merged record describes the decision as it was
  actually realized.

- Blocking RFCs MUST be resolved.

  Every RFC listed under `Depends on` is itself implemented.

- You MUST NOT mark an RFC implemented until the tooling and infrastructure
  it calls for are genuinely in place.

  That is what keeps the archive honest.

- You MUST NOT change RFC document fields other than `Status`, `Last
  updated`, cross-references, and implementation trackers once merged.

  Once merged at `#implemented`, only the `Status` field, `Last updated`
  date, cross-references to related RFCs, and implementation trackers may
  change.

- You MUST push before merging.

  `gh pr merge` merges what is on the remote. A status change committed
  locally but not pushed is silently dropped from `main`, leaving the merged
  RFC still reading `ACCEPTED`.

- You MUST NOT merge without explicit instruction from the user.
