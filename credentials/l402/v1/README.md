# L402 Access Credential Schema

Binds DID identity with payment proof and scoped access authorization for payment-gated services.

## Schema

### [l402-access.json](l402-access.json)

Express that a DID holder has paid for and is authorized to access specific services within defined scope and rate limits.

**Use case:** An AI advisor pays a Lightning invoice to subscribe to a node's management API. The node issues an L402 Access Credential binding the advisor's DID to the payment proof and a scoped set of allowed actions with rate limits.

**Core fields:**
- `accessType` — Access domain identifier (e.g., `hive:management`, `api:read`)
- `paymentProof` — Payment method (`lightning` or `cashu`), preimage hash, macaroon, token reference, amount, and timestamp
- `scope` — Allowed schemas, maximum actions, and rate limits
- `macaroonCaveats` — L402 macaroon caveats binding access to specific conditions (DID, tier, expiration, etc.)

## Payment Models

| Model | Payment Proof | Scope | Use Case |
|-------|--------------|-------|----------|
| **Per-action (Cashu)** | Cashu token hash + mint URL | Single action | Low-volume, pay-as-you-go |
| **Subscription (L402)** | Lightning preimage hash + macaroon | N actions over time window | High-volume, predictable access |
| **Hybrid** | Both methods accepted | Varies | Flexible access patterns |

## Macaroon Caveats

L402 macaroons support attenuation via caveats. Common caveats for service access:

| Caveat | Example Value | Purpose |
|--------|--------------|---------|
| `did` | `did:cid:bagaaiera...` | Bind to specific DID holder |
| `tier` | `standard` | Permission tier |
| `expires` | `2026-03-14T00:00:00Z` | Expiration timestamp |
| `max_actions` | `1000` | Action budget |
| `service` | `hive:management` | Service domain restriction |

## Design

- **W3C VC 2.0** compliant
- **Domain-agnostic** — works for any payment-gated service, not just Lightning management
- **Composable** with [Service Credentials](../service/v1/) for delegation scope and [Escrow Receipts](../escrow/v1/) for conditional payment proof

## Related

- [Archon Issue #75](https://github.com/nicholasgasior/gatekeeper/issues/75) — L402 integration with Archon Gatekeeper
- [DID + L402 Remote Fleet Management](https://github.com/lightning-goats/cl-hive/blob/main/docs/planning/DID-L402-FLEET-MANAGEMENT.md) — Full specification for authenticated, paid remote node management

## Contributing

When using L402 access credentials with new service domains:
- Define the `accessType` namespace:type identifier
- Document which `macaroonCaveats` are meaningful for the domain
- Specify rate limiting expectations for the service
