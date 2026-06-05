---
name: supersede-rfc
description: Supersede a previously-accepted RFC by a newer one. Use this skill when the user says "supersede this RFC", "this RFC is replaced by ...", or retires an accepted decision in favor of a newer one.
license: MIT
---

# Supersede RFC

Use this skill to transition an RFC from `IMPLEMENTED` to `SUPERSEDED`, once a later, implemented RFC has replaced its decision. This is the only transition out of `IMPLEMENTED`. The superseded document remains in `rfc/` permanently as part of the historical record.

Do NOT use this skill for any other transition — see [`accept-rfc`](../accept-rfc/SKILL.md), [`implement-rfc`](../implement-rfc/SKILL.md), [`reject-rfc`](../reject-rfc/SKILL.md), [`propose-rfc`](../propose-rfc/SKILL.md), or [`draft-rfc`](../draft-rfc/SKILL.md).

## Transition gates: `IMPLEMENTED` → `SUPERSEDED`

The RFC being superseded MUST currently be `IMPLEMENTED`. Confirm _all_ of the following before superseding. If any is unmet, report it and pause.

-   **A later RFC has replaced this decision.**

    That successor RFC is itself `IMPLEMENTED` — a draft, proposed, accepted, or rejected RFC cannot supersede an implemented one, because its replacement tooling and infrastructure are not yet in place. The successor MUST be the newer of the two (a higher `rfc/INDEX.md` number).

-   **The cross-references are reciprocal.**

    The superseded RFC's `Superseded by` field links the successor, and the successor's `Supersedes` field links back to this one.

##  Instructions

1.  **Identify both RFCs.**

    The implemented RFC being superseded, and the later implemented RFC that replaces it. Ask the user for the RFC being superseded and the newer one that replaces it.

    If the user gave a short description (eg. "X is superseded by Y"), use it to infer both.

    Confirm both are `IMPLEMENTED` and that the successor is the newer of the two.

2.  **Verify the transition rules above.**

    Report any unmet gate and stop.

3.  **Update the superseded document and the index.**

    - Set `Status` to `SUPERSEDED` and `Last updated` to today's date.
    - Set the `Superseded by` cross-reference to the successor RFC.
    - In [`rfc/INDEX.md`](../../../rfc/INDEX.md), change this RFC's row status to `Superseded`.

    Change nothing else in the document — it is otherwise immutable.

4.  **Confirm the successor links back.**

    Ensure the successor RFC's `Supersedes` field references this RFC. The successor is edited through its own pull request; if the back-link is missing, flag it.

5.  **Switch the state label on the old RFC.**

    On the superseded RFC's original pull request:

    ```sh
    gh pr edit <number> --add-label "#superseded" --remove-label "#implemented"
    ```

6.  **Land the document change.**

    Commit the edit to the superseded document — typically as part of the superseding RFC's pull request, since `main` is updated only through pull requests:

    ```sh
    git commit -am "supersede: <short lowercase description of superseded rfc>"
    ```

##  Rules

-   **Only from `IMPLEMENTED`.**

    A draft, proposed, accepted, or rejected RFC cannot be superseded.

-   **Immutable except the cross-reference.**

    Only the `Status` field, `Last updated` date, and the `Superseded by` link may change.

## Success criteria

- `Status` is `SUPERSEDED`, `Last updated` is today's date, and `Superseded by` links the successor.

- The successor's `Supersedes` field links back to this RFC.

- The PR carries `#superseded` (and its category label).

## References

- [`AGENTS.md`](../../../AGENTS.md): The full RFC lifecycle and immutability rules.

- [`implement-rfc`](../implement-rfc/SKILL.md): How both the superseded RFC and its successor reached `#implemented`.
