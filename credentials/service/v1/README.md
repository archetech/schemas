# Service Credential Schemas

General-purpose schemas for delegated service relationships between DIDs — scoped authorization and service advertising.

## Schemas

### [service-credential.json](service-credential.json)

Express a scoped delegation of authority from one DID to another within a specific service domain.

**Use case:** A Lightning node operator issues a service credential to an AI advisor, granting permission to adjust fees and rebalance channels within defined constraints and compensation terms.

**Core fields:**
- `serviceType` — Domain identifier (e.g., `hive:management`, `agent:code-review`)
- `delegator` — DID granting authority (issuer)
- `delegate` — DID receiving authority (subject)
- `permissions` — Boolean flags for authorized actions
- `constraints` — Quantitative limits (rate limits, amount caps, allowed schemas)
- `tier` — Named permission level
- `compensation` — Payment model, rate, currency, and escrow terms
- `scope` — Additional metadata (allowed schemas, target resources, daily action limits)

### [service-profile.json](service-profile.json)

Advertise service capabilities, pricing, and availability. Self-issued by service providers to enable marketplace discovery.

**Use case:** An AI fleet advisor publishes a service profile describing their routing optimization capabilities, pricing models, current availability, and links to reputation credentials from past clients.

**Core fields:**
- `serviceType` — Service domain identifier
- `capabilities` — What the provider can do
- `supportedSchemas` — Which command schemas the provider supports
- `pricing` — Available compensation models with rates
- `availability` — Capacity, current load, acceptance status
- `specializations` — Areas of particular expertise
- `reputation` — References to third-party reputation credentials
- `contact` — DID and endpoints for communication

## Service Types

Service type identifiers follow the `namespace:type` pattern:

| Service Type | Description | Example Use |
|-------------|-------------|-------------|
| `hive:management` | Lightning fleet management | AI advisor managing node fees, rebalancing, channels |
| `hive:monitoring` | Node health monitoring | Dashboard service tracking uptime and metrics |
| `agent:code-review` | Code review service | AI agent reviewing pull requests |
| `infra:monitoring` | Infrastructure monitoring | Service monitoring uptime and alerting |

New service types are created organically — any issuer can define a new `namespace:type` pair.

## Design

- **W3C VC 2.0** compliant (`validFrom`/`validUntil`, standard context)
- **Domain-agnostic** — the same schema works for Lightning fleet management, code review, or any delegated service
- **Composable** with [Reputation Credentials](../reputation/v1/) for trust evaluation and [Escrow Receipts](../escrow/v1/) for payment conditionality

## Design Documents

- [DID + L402 Remote Fleet Management](https://github.com/lightning-goats/cl-hive/blob/main/docs/planning/DID-L402-FLEET-MANAGEMENT.md) — Full specification for authenticated, paid remote node management
- [DID Hive Marketplace Protocol](https://github.com/lightning-goats/cl-hive/blob/main/docs/planning/DID-HIVE-MARKETPLACE.md) — Marketplace layer for service discovery, negotiation, and contracting

## Contributing

When proposing new service types:
- Follow the `namespace:type` naming convention
- Define clear permission semantics for the domain
- Document expected constraint keys and their units
- Specify which compensation models are appropriate
