---
name: implement-rfc
description: Mark an accepted RFC as implemented once its tooling and infrastructure are in place. Squash-merge its pull request and assign its number in the index. Use when the user says "implement this RFC", "this RFC is implemented", "the tooling is in place", or "the infrastructure is built".
license: MIT
---

# Implement RFC

Use this skill to transition an RFC from `ACCEPTED` to `IMPLEMENTED`, once all the tooling and infrastructure the decision calls for are in place. This is the point at which the RFC's pull request is squash-merged into `main` and the RFC is assigned its number in the [RFC index](../../../rfc/INDEX.md).

An accepted RFC is a settled decision whose pull request stays open through the implementation phase.

Do NOT use this skill for any other transition — to accept use [`accept-rfc`](../accept-rfc/SKILL.md), to retire an implemented decision use [`supersede-rfc`](../supersede-rfc/SKILL.md), to reject use [`reject-rfc`](../reject-rfc/SKILL.md), and to scaffold or propose use [`draft-rfc`](../draft-rfc/SKILL.md) / [`propose-rfc`](../propose-rfc/SKILL.md).

## Transition gates: `ACCEPTED` → `IMPLEMENTED`

The RFC MUST currently be `ACCEPTED` (a PR carrying `#accepted`). Confirm _all_ of the following before implementing. If any is unmet, report it and pause.

-   **The tooling and infrastructure are in place.**

    Everything the decision calls for — the tools, automation, infrastructure, configuration, or conventions — has actually been built and put into effect, not merely planned.

-   **The RFC document reflects the decision as carried out.**

    Any drift discovered during implementation has been reconciled back into the document, so the merged record describes the decision as it was actually realized.

-   **Blocking RFCs are resolved.**

    Every RFC listed under `Depends on` is itself implemented.

## Instructions

1.  **Identify the RFC and confirm it is `ACCEPTED`.**

    Infer the target from the current checked-out branch (`rfc/<slug>`). If on `main`, use the user's description to infer the target RFC if they gave one, otherwise list the open `#accepted` pull requests and ask the user to choose:

    ```sh
    gh pr list --label "#accepted" --json number,title,headRefName
    ```

    Read the document. Check `Status` is `ACCEPTED` and the PR carries `#accepted` (`gh pr view <number> --json labels`).

2.  **Verify the transition gates.**

    Report any unmet gate and stop.

3.  **Update the document.**

    - Set `Status` to `IMPLEMENTED` and `Last updated` to today's date.
    - Confirm `Implementation trackers` are linked.

4.  **Switch the state label.**

    ```sh
    gh pr edit <number> --add-label "#implemented" --remove-label "#accepted"
    ```

    This swaps only the lifecycle label. Leave the category label, eg. `TOOLING`, in place.

5.  **Commit.**

    ```sh
    git commit -am "implement: <short lowercase rfc description>"
    ```

6.  **Merge the pull request.**

    The RFC document is now ready to land on `main`. Confirm with the user that the PR is ready to merge — do not merge without explicit instruction. Once confirmed, squash-merge it with the message `rfc: <short lowercase rfc description> - IMPLEMENTED`:

    ```sh
    gh pr merge <number> --squash --subject "rfc: <short lowercase rfc description> - IMPLEMENTED"
    ```

7.  **After merge, assign the number.**

    The RFC number is assigned only after merge. On `main`, find the highest number in [RFC index](../../../rfc/INDEX.md), increment by one, zero-pad to four digits (eg. `0006` → `0007`), and add a row for this RFC — its number, title, category, `IMPLEMENTED` status, the RFC's `Decision date` (its approval date), and a link to its directory (`rfc/<category>/<slug>/`).

    Commit this directly to `main`, and push:

    ```sh
    git commit -am "chore: assign rfc <number>"
    git push
    ```

    An implemented RFC stays in effect until a later RFC supersedes it.

## Rules

-   **Only from `ACCEPTED`.**

    Never implement a draft, proposed, or rejected RFC.

-   **Implemented means built.**

    Do not mark an RFC implemented until the tooling and infrastructure it calls for are genuinely in place — that is what keeps the archive honest.

-   **RFCs are immutable after merge.**

    Once merged at `#implemented`, only the `Status` field, `Last updated` date, cross-references to related RFCs, and implementation trackers may change.

-   **Do not merge without explicit instruction.**

## Success criteria

- `Status` is `IMPLEMENTED` and `Last updated` is today's date.

- The PR carries `#implemented` (and its category label), not `#accepted`.

- The RFC document is squash-merged into `main`.

- After merge: an `rfc/INDEX.md` entry is added on `main`, with the next sequential number and `Implemented` status.

## References

- [`AGENTS.md`](../../../AGENTS.md): The full RFC lifecycle and immutability rules.
