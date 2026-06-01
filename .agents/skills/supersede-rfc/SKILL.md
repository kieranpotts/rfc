---
name: supersede-rfc
description: Mark an accepted RFC as superseded once a later RFC has replaced its decision. Use when the user says "supersede this RFC", "this RFC is replaced by ...", or retires an accepted decision in favor of a newer one.
license: MIT
---

# Supersede RFC

Use this skill to move an RFC from **accepted** to **superseded**, once a later, accepted RFC has replaced its decision. This is the only transition out of `ACCEPTED`. The superseded document remains in `rfcs/` permanently as part of the historical record.

Do NOT use this skill for any other transition — see [`approve-rfc`](../approve-rfc/SKILL.md), [`reject-rfc`](../reject-rfc/SKILL.md), [`propose-rfc`](../propose-rfc/SKILL.md), or [`draft-rfc`](../draft-rfc/SKILL.md).

## Transition rules (accepted → superseded)

The RFC being superseded MUST currently be `ACCEPTED`. Confirm **all** of the following before superseding. If any is unmet, report it and pause.

-   **A later RFC has replaced this decision**, and that successor RFC is itself `ACCEPTED` — a proposed or rejected RFC cannot supersede an accepted one.
-   **The cross-references are reciprocal:** the superseded RFC's `Superseded by` field links the successor, and the successor's `Supersedes` field links back to this one.
-   **Only maintainers may supersede.** If there is any indication the current user is not a maintainer, ask for confirmation first.

## Instructions

1.  **Identify both RFCs.**

    The accepted RFC being superseded, and the later accepted RFC that replaces it. Confirm the older one is `ACCEPTED`.

2.  **Verify the transition rules above.**

    Report any unmet gate and stop.

3.  **Update the superseded document.**

    - Set `Status` to `SUPERSEDED` and `Last updated` to today's date.
    - Set the `Superseded by` cross-reference to the successor RFC.
    - Change nothing else — the document is otherwise immutable.

4.  **Confirm the successor links back.**

    Ensure the successor RFC's `Supersedes` field references this RFC. The successor is edited through its own pull request; if the back-link is missing, flag it.

5.  **Apply the label.**

    On the superseded RFC's original pull request:

    ```sh
    gh pr edit <number> --add-label "#superseded" --remove-label "#accepted"
    ```

    This swaps only the lifecycle label; leave the category label in place.

6.  **Land the document change.**

    Commit the edit to the superseded document — typically as part of the superseding RFC's pull request, since `main` is updated only through pull requests:

    ```sh
    git commit -am "rfc: supersede <NNNN>-<slug>"
    ```

## Rules

-   **Only maintainers may supersede.** If unsure of the user's role, ask first.

-   **Only from `ACCEPTED`.** A draft, proposed, or rejected RFC cannot be superseded.

-   **Immutable except the cross-reference.** Only the `Status` field, `Last updated` date, and the `Superseded by` link may change.

## Success criteria

-   **`Status` is `SUPERSEDED`**, `Last updated` is today's date, and `Superseded by` links the successor.

-   **The successor's `Supersedes` field links back** to this RFC.

-   **The PR carries `#superseded`** (and its category label).

## References

- [AGENTS.md](../../../AGENTS.md): The full RFC lifecycle and immutability rules.

- [`approve-rfc`](../approve-rfc/SKILL.md): How the superseding RFC was accepted.
