# RFCs

This directory is the permanent archive of every major technical decision proposed for this project, including those that were ultimately rejected.

Nothing here is ever deleted. It's an immutable, append-only log of historical technical decisions. Importantly, rejected and superseded RFCs remain in place, as a record of the original decision and its rationale, so the same ground is not needlessly covered again later.

## Layout

Each RFC is a directory, grouped by category:

```
rfc/
├── INDEX.md          # The catalog of every RFC, with its number.
├── TEMPLATE.md       # The starting point for a new RFC.
├── architecture/
├── process/
├── technology/
└── tooling/
    └── <slug>/
        ├── README.md # The main RFC document.
        └── …         # Diagrams or other supporting artifacts.
```

An RFC's directory holds its `README.md` (the proposal itself, copied from [`TEMPLATE.md`](./TEMPLATE.md)) plus any supporting artifacts — diagrams, data, prototypes.

See the [contributing guidelines](../CONTRIBUTING.md) for details of the process to create new RFCs, and the [agent skills](../.agents/skills/) that can be used to automate it.
