# Memeplex schemas

Schemas for [Memeplex](https://github.com/archetech/archon/blob/main/docs/plans/memeplex-1436.md), a protocol for publishing on Archon in which every object is a DID. They describe asset data, not credentials: a schema validates the `memeplex`, `memeplexGrant` or `memeplexGrantRequest` member of an asset's data.

The [Memeplex reference](https://github.com/archetech/archon/blob/main/docs/plans/memeplex-reference-1436.md) is normative. It holds the text of each schema and three checks a schema cannot express: a rating's bounds, a paper's `authors` including its `author`, and an expiry being a real instant. The files here are that text, each with `$schema` and the definitions it refers to, so that each stands alone.

Memeplex is a design and is not implemented. These schemas are not published yet. When they are, each DID and `versionId` is recorded below, and the schemas for `v: 1` do not change after that: a change to what is valid is a new `v`.

## Objects

| Kind | Schema | What it is |
|---|---|---|
| `post` | [post.json](post.json) | A post, an article when it has a `title`, or a boost or quote post when it has a `target` |
| `paper` | [paper.json](paper.json) | A paper, revised in place, with its listed authors and optional PDF and source |
| `reply` | [reply.json](reply.json) | A reply, or a review when it has a `verdict` |
| `rating` | [rating.json](rating.json) | A score on a scale the rating states |
| `tag` | [tag.json](tag.json) | A label, a reaction, or a custom emoji when it has an `image` |

## Grants

| Schema | What it is |
|---|---|
| [grant.json](grant.json) | A user's authorization for one client to publish as them (`memeplexGrant`) |
| [grant-request.json](grant-request.json) | What a client presents to a wallet to ask for a grant (`memeplexGrantRequest`) |

## Published as

Not yet published.

## Testing

The Archon repository holds the same files in `share/schema/memeplex/v1`, a test that keeps them equal to the reference's text, and signed objects, valid and invalid, in `tests/fixtures/memeplex-v1-vectors.json`.
