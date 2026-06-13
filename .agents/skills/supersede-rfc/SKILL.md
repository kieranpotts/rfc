---
name: supersede-rfc
description: Supersede a previously-accepted RFC by a newer one. Use this skill when the user says "supersede this RFC", "this RFC is replaced by ...", or retires an accepted decision in favor of a newer one.
license: MIT
---

# `/supersede-rfc`

Use this skill to transition an RFC from `IMPLEMENTED` to `SUPERSEDED`, once a later, implemented RFC has replaced its decision. The superseded document remains in `rfc/` permanently as part of the historical record.

Do NOT use this skill for any other transition — see [`/accept-rfc`](../accept-rfc/SKILL.md), [`/implement-rfc`](../implement-rfc/SKILL.md), [`/reject-rfc`](../reject-rfc/SKILL.md), [`/propose-rfc`](../propose-rfc/SKILL.md), or [`/draft-rfc`](../draft-rfc/SKILL.md).

## Transition gates: `IMPLEMENTED` → `SUPERSEDED`

The RFC being superseded MUST currently be `IMPLEMENTED`. Confirm _all_ of the following before superseding. If any is unmet, report it and pause.

-   **Both RFCs are in the `main` branch.**

    Both the succeeded and the successor RFC MUST have previously been merged into the `main` branch.

-   **Both have a unique RFC number**

    The two RFCs MUST each have a unique RFC number assigned in the [RFC index](../../../rfc/INDEX.md).

-   **Both are implemented.**

    Both the succeeded RFC and its successor MUST currently be `IMPLEMENTED`. A draft, proposed, accepted, or rejected RFC cannot supersede an implemented one, because its replacement tooling and infrastructure are not yet in place.

-   **The successor is the newer of the two RFCs.**

    The successor MUST be the newer of the two. It MUST have a higher RFC number in the [RFC index](../../../rfc/INDEX.md) number.

##  Instructions

1.  **Identify both RFCs.**

    Identify the implemented RFC being superseded, and the later implemented RFC that replaces it. If the user gave a short description (eg. "X is superseded by Y"), use it to infer both. Else prompt the user.

2.  **Verify the transition gates.**

    Report any unmet gate and stop.

3.  **Point the successor to the succeeded RFC.**

    Update the successor's RFC document's `Supersedes` field to link back to the succeeded RFC document, referenced by its RFC index number.

4.  **Point the succeeded RFC to its successor.**

    Update the succeeded RFC's `Superseded by` field to link to the successor RFC, referenced by its RFC index number.

    Set `Status` to `SUPERSEDED` and `Last updated` to today's date.

    In the [RFC index](../../../rfc/INDEX.md), change the succeeded RFC's row status to `SUPERSEDED`.

    Change nothing else in the document — it is otherwise immutable.

5.  **Land the document change.**

    Commit the edits to both documents at the same time. This can be done directly on `main`:

    ```sh
    git commit -am "supersede: <short lowercase description of superseded rfc>"
    ```

6.  **Switch the state label on the old RFC pull request.**

    On the superseded RFC's original pull request:

    ```sh
    gh pr edit <number> --add-label "#superseded" --remove-label "#implemented"
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
