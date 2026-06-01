---
name: audit-rfc
description: Check an RFC document for completeness, consistency, and process compliance. Use when the user wants to review an RFC before advancing it, says "check this RFC", "review this RFC", or "is this RFC ready to advance?".
license: MIT
---

# Audit RFC

Use this skill to sanity-check an RFC before it advances to the next lifecycle state. It verifies that required fields are filled in, the document is internally consistent, the GitHub label and document `Status` field agree, and cross-references resolve.

Do NOT use this skill to advance an RFC's state (use [`advance-rfc`](../advance-rfc/SKILL.md)) or to scaffold a new RFC (use [`draft-rfc`](../draft-rfc/SKILL.md)).

## Instructions

1.  **Identify the RFC to check.**

    If the user does not specify, look for the most recently modified file in `rfcs/` (excluding `TEMPLATE.md` and `README.md`), or ask.

2.  **Check the metadata header.**

    Verify that the following fields are filled in and non-placeholder:

    - `Authors`: At least one name present.
    - `Created` and `Last updated`: Valid `YYYY-MM-DD` dates; `Last updated` is not older than `Created`.
    - `Status`: One of `DRAFT`, `PROPOSED`, `ACCEPTED`, `REJECTED`, `SUPERSEDED`.
    - `PR`: Either a linked PR number or a note that the PR is not yet open (acceptable for `DRAFT`).

3.  **Check the labels.**

    If a PR number is present, run:

    ```sh
    gh pr view <number> --json labels,state
    ```

    Confirm both of the following:

    - The PR carries exactly one category label — `ARCHITECTURE`, `PROCESS`, `TECHNOLOGY`, or `TOOLING`. A missing or duplicate category label is a gate failure.
    - The PR carries a lifecycle label matching the document's `Status` field (eg. `#proposed` when `Status: PROPOSED`).

4.  **Check the required prose sections.**

    Each of the following sections must be present and contain substantive content (not just the placeholder text from `TEMPLATE.md`):

    - `Summary`: A concise single-paragraph description of the decision.
    - `Motivation`: Explains the problem being solved and for whom.
    - `Impact`: One of `HIGH`, `MEDIUM`, or `LOW`, plus a description of what is affected.
    - `Proposed change`: Describes the solution in enough detail to evaluate.
    - `Alternatives`: At least one alternative considered.
    - `Trade-offs and risks`: Honest about downsides.

5.  **Check cross-references.**

    For each value in the `Related RFCs` section (`Supersedes`, `Superseded by`, `Depends on`, `Related to`):

    - If the reference is an RFC number, confirm the corresponding `NNNN-*.md` file exists in `rfcs/`.
    - If the reference is a GitHub issue or PR number, it need not be verified locally, but note any that look malformed.

6.  **Report findings.**

    Produce a summary with two sections:

    - **Passes**: A bullet list of checks that passed.
    - **Failures / warnings**: A bullet list of anything that needs attention, with a brief explanation for each.

    Do not advance the RFC or make any changes. Report only.

## Rules

-   **Report, do not fix.**

    This skill is an auditor, not an editor. Surface findings and let the proposer or maintainer decide how to address them.

-   **Distinguish failures from warnings.**

    A *failure* is a gate that must be resolved before the RFC can advance. A *warning* is a quality concern that does not block advancement but should be noted.

-   **Check all sections, even if early ones fail.**

    Run the full audit before reporting. A partial report is less useful than a complete one.

## Success criteria

-   **Every check listed in the instructions has been performed.**

-   **The report clearly separates passes from failures/warnings.**

-   **No changes were made** to any file in the repository.

-   **Each failure names the specific field, section, or file** that did not pass, with enough detail for the proposer to act on it.

## References

- [AGENTS.md](../../../AGENTS.md): Describes the state machine and gate conditions, optimized for agent discovery.

- [PR checklist](../../../.github/PULL_REQUEST_TEMPLATE.md): The authoritative checklist of gates per state transition.

- [`rfcs/TEMPLATE.md`](../../../rfcs/TEMPLATE.md): Reference for required fields and sections.

- [`advance-rfc`](../advance-rfc/SKILL.md): `advance-rfc` depends on this skill — an audit must pass before an RFC can be advanced to a new state.
