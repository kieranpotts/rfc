# Agent skills for managing Requests for Comments (RFCs)

The skills available to agents in this project are:

- **[scaffold-rfc](./scaffold-rfc/):** \
  Scaffolds a new RFC, ready for the user to complete.
  Sets the status to `DRAFT`.

- **[propose-rfc](./propose-rfc/):** \
  Handles the `DRAFT` → `PROPOSED` transition.

- **[accept-rfc](./accept-rfc/):** \
  Handles the `PROPOSED` → `ACCEPTED` transition.

- **[implement-rfc](./implement-rfc/):** \
  Handles the `ACCEPTED` → `IMPLEMENTED` transition.

- **[reject-rfc](./reject-rfc/):** \
  Handles the `PROPOSED` → `REJECTED` transition.

- **[supersede-rfc](./supersede-rfc/):** \
  Handles the `IMPLEMENTED` → `SUPERSEDED` transition.

The **scaffold-rfc** skill....

```mermaid
flowchart LR
  scaffold["🤖<br/>scaffold"]:::agentic
  propose["🤖<br/>propose"]:::agentic
  accept["🤖<br/>accept"]:::agentic
  reject["🤖<br/>reject"]:::agentic
  implement["🤖<br/>implement"]:::agentic
  supersede["🤖<br/>supersede"]:::agentic

  scaffold ==> propose
  propose ==> accept
  accept ==> implement
  implement ==> supersede
  propose -.-> reject
  accept -.-> reject

  classDef agentic fill:#cce5ff,stroke:#004085,color:#004085,stroke-width:2px
  classDef scripted fill:#e2e3e5,stroke:#4b5157,color:#383d41,stroke-width:2px
  classDef anthropic fill:#fff3cd,stroke:#856404,color:#856404,stroke-width:2px,stroke-dasharray:2 3
```

## Compatibility

These skills are compatible with the [Agent Skills](https://agentskills.io/)
convention. Most agent harnesses support this convention natively, but
workarounds may be required for harnesses that do not.
