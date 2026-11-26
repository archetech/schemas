# Escrow Receipt Schema

Signed proof-of-completion credential for conditional task escrow using Cashu ecash tokens.

## Schema

### [escrow-receipt.json](escrow-receipt.json)

Record the outcome of a delegated task executed under escrow conditions, including whether payment was released.

**Use case:** A Lightning node executes a rebalancing task requested by an AI advisor. The node issues an escrow receipt recording success, the HTLC preimage revelation (releasing payment), and metrics like the amount rebalanced and routing fees paid.

**Core fields:**
- `taskId` — Unique task identifier
- `taskSchema` — Schema of the executed task (e.g., `hive:rebalance/v1`)
- `executor` — DID of the agent that performed the task
- `verifier` — DID of the node/oracle that verified completion
- `completedAt` — Completion timestamp
- `result` — Outcome: `success`, `partial`, or `failed`
- `preimageRevealed` — Whether the HTLC preimage was revealed (payment released)
- `metrics` — Domain-specific quality measurements
- `stateHashBefore` / `stateHashAfter` — State integrity proofs
- `evidence` — Supporting attestations and receipts

## Escrow Flow

1. **Operator** mints a Cashu escrow ticket (P2PK + HTLC + timelock)
2. **Agent** presents ticket + credential + task command to the node
3. **Node** executes the task and issues this receipt
4. On **success**: receipt includes the HTLC preimage; agent redeems the token
5. On **failure**: no preimage; operator reclaims via timelock refund

The receipt serves as verifiable evidence for [Reputation Credentials](../reputation/v1/) — completed escrow receipts prove an agent's track record.

## Design

- **W3C VC 2.0** compliant
- **Domain-agnostic** — works for any task schema, not just Lightning operations
- **Evidence-backed** — links to signed receipts, metric snapshots, and audit logs
- **Composable** with [Service Credentials](../service/v1/) for delegation scope and [L402 Access Credentials](../l402/v1/) for payment proof

## Design Document

- [DID + Cashu Task Escrow Protocol](https://github.com/lightning-goats/cl-hive/blob/main/docs/planning/DID-CASHU-TASK-ESCROW.md) — Full specification for conditional Cashu ecash tokens as task escrow tickets

## Contributing

When using escrow receipts with new task domains:
- Define meaningful `metrics` keys for the domain
- Document what constitutes `success` vs `partial` vs `failed` for the task schema
- Ensure the verifier is an objective party (or document the trust assumption)
