# Agent Credential Schemas

Pre-built credential schemas for AI agent use cases.

## Schemas

### [collaboration-partner.json](collaboration-partner.json)
Attest to collaboration relationships between agents and/or humans.

`did:cid:bagaaieraphn3fzvf3m5l56xasfwout6yilhx5snepvirjy3gin4b3ybtbwyq`

**Use case:** Agent A issues credential to Agent B attesting they work together on a project.


### [capability-attestation.json](capability-attestation.json)
`did:cid:bagaaierajqpms3pg4jnacor7fdci52rg3aj33abzyp5v5djnhbzgxhgoipia`

Attest to specific capabilities or competencies of an agent.

**Use case:** A human attests that an agent can manage Lightning nodes at an "advanced" level.



### [infrastructure-authorization.json](infrastructure-authorization.json)

`did:cid:bagaaieraarhb7r43das5lxx5ki6besumyu7qytwesvmkjxtgpoliw54x2xwq`

Infrastructure (nodes, servers) attesting agent authorization.

**Use case:** A Lightning node signs a message authorizing an agent to manage it.

### [identity-link.json](identity-link.json)

`did:cid:bagaaierasl6iztpjykhtspgpfbse5ctajlqdqsfolzbsqhh5ncoyv7otvlla`

Link an Archon DID to identity on another platform (Nostr, Lightning, GitHub, etc.).

**Use case:** Agent proves same identity controls both their Archon DID and Nostr npub.

## Contributing

These schemas are designed for the emerging ecosystem of AI agents using Archon for decentralized identity. Contributions welcome!

When adding new schemas:
- Follow JSON Schema draft-07
- Include clear descriptions for all fields
- Mark truly required fields as required
- Document use cases in this README
