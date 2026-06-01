# Skills

These on-demand agent skills manage the RFC workflow — one per state transition in the lifecycle (`draft → proposed → accepted | rejected`, and `accepted → superseded`):

- [`draft-rfc`](./draft-rfc/): Scaffold a new RFC and open it as a draft pull request.

- [`propose-rfc`](./propose-rfc/): Remove a PR's draft status, marking the RFC ready for review.

- [`approve-rfc`](./approve-rfc/): Approve a proposed RFC — assign its ID and accept it.

- [`reject-rfc`](./reject-rfc/): Reject a proposed RFC, preserving it permanently as a record.

- [`supersede-rfc`](./supersede-rfc/): Mark an accepted RFC as superseded by a later one.

Each skill carries the rules for its own transition; there is no separate audit step.
