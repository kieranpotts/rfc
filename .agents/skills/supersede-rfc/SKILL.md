---
name: supersede-rfc
description: >-
  Supersede a previously-accepted RFC with a newer one. Use this skill when
  the user says something like "supersede this RFC", "this RFC is replaced by ...",
  "supersede RFC", "<topic> is superseded by <successor>", or otherwise
  wishes to retire an accepted decision in favor of a newer one.
license: CC0-1.0
metadata:
  interactive: yes
  preferred_model: ollama/WORKFLOW_BASIC
---

# Supersede RFC

Use this skill to transition an RFC from `IMPLEMENTED` to `SUPERSEDED`, once
a later, implemented RFC has replaced its decision. The superseded document
remains in `rfc/` permanently as part of the historical record.

## Parameters

Determine the following information from the surrounding context and
environment, if possible.

- **The succeeded RFC and its successor — REQUIRED.** Infer both from the user's
  description (eg. "X is superseded by Y"), or prompt for them.

## Success criteria

You will achieve the following outcomes:

<!-- The succeeded RFC's document updated to `Status: SUPERSEDED` with a
`Superseded by` link, the successor's `Supersedes` field linked back, the
`rfc/INDEX.md` row updated, and the old PR carrying `#superseded`. -->

- `Status` MUST be `SUPERSEDED`, `Last updated` MUST be today's date, and
  `Superseded by` MUST link the successor.

- The successor's `Supersedes` field MUST link back to this RFC.

- The PR MUST carry `#superseded` (and its category label).

## Instructions

1.  Identify both RFCs.

    Identify the implemented RFC being superseded, and the later implemented
    RFC that replaces it. If the user gave a short description (eg. "X is
    superseded by Y"), use it to infer both. Else prompt the user.

2.  Verify the rules.

    Report any unmet rule and stop.

3.  Point the successor to the succeeded RFC.

    Update the successor's RFC document's `Supersedes` field to link back to
    the succeeded RFC document, referenced by its RFC index number.

4.  Point the succeeded RFC to its successor.

    Update the succeeded RFC's `Superseded by` field to link to the successor
    RFC, referenced by its RFC index number.

    Set `Status` to `SUPERSEDED` and `Last updated` to today's date.

    In the [RFC index](../../../rfc/INDEX.md), change the succeeded RFC's row
    status to `SUPERSEDED`.

    Change nothing else in the document — it is otherwise immutable.

5.  Land the document change.

    Commit the edits to both documents and the index row at the same time,
    directly to `main`, and push. Both RFCs are already merged, and every
    field touched here is one of the few a merged RFC may still change — so
    there is nothing for a pull request to review:

    ```sh
    git checkout main
    git pull --rebase
    git commit -am "supersede: <short lowercase description of superseded rfc>"
    git push
    ```

    The push is mandatory. An unpushed supersession leaves the archive
    claiming the old RFC is still in effect.

6.  Switch the state label on the old RFC pull request.

    On the superseded RFC's original pull request:

    ```sh
    gh pr edit <number> --add-label "#superseded" --remove-label "#implemented"
    ```

## Rules

- You MUST NOT supersede an RFC that is not currently `IMPLEMENTED`.

  A draft, proposed, accepted, or rejected RFC cannot be superseded.

- Both RFCs MUST be in the `main` branch.

  Both the succeeded and the successor RFC MUST have previously been merged
  into the `main` branch.

- Both MUST have a unique RFC number.

  The two RFCs MUST each have a unique RFC number assigned in the
  [RFC index](../../../rfc/INDEX.md).

- Both MUST be implemented.

  Both the succeeded RFC and its successor MUST currently be `IMPLEMENTED`.
  A draft, proposed, accepted, or rejected RFC cannot supersede an
  implemented one, because its replacement tooling and infrastructure are
  not yet in place.

- The successor MUST be the newer of the two RFCs.

  It MUST have a higher RFC number in the
  [RFC index](../../../rfc/INDEX.md).

- The cross-reference change MUST be committed directly to `main`, and
  pushed.

  Both RFCs are already merged. The only fields this skill touches —
  `Status`, `Last updated`, `Superseded by`, `Supersedes`, and the index row
  — are among the few a merged RFC may still change, so a pull request would
  have nothing to review. This matches how RFC numbers are assigned at
  implementation and rejection, which also commit straight to `main`.

- You MUST NOT change RFC document fields other than `Status`, `Last
  updated`, and `Superseded by` when superseding.

  Only the `Status` field, `Last updated` date, and the `Superseded by` link
  may change.
