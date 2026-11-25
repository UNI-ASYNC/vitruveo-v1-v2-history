# Protocol Changes Identified in the V1 → V2 Review

This page records meaningful differences identified in preserved source-comparison research. It is an initial review, not an exhaustive feature inventory.

## Client foundation and repository lineage
The V2 client is based on Geth v1.13.15, while the V1-era source was recorded as Geth v1.13.0. The two Vitruveo repositories have separate histories. This is a client-foundation transition, not merely a small patch series within one repository.

- [V1-era source](https://github.com/Vitruveo/vitruveo-protocol-dev)
- [V1 reviewed commit c4d5b01](https://github.com/Vitruveo/vitruveo-protocol-dev/commit/c4d5b01cb5f039964bed2a0416110885ffafc37)
- [V2 source](https://github.com/Vitruveo/vitruveo-protocol)
- [V2 reviewed commit ba0ef28d](https://github.com/Vitruveo/vitruveo-protocol/commit/ba0ef28d9844b84cd114b638b541c241af33e345)

## Rebase address changed to RNG
The V1-era client used the `0x…FF` precompile address for Rebase-related functionality. The V2 source reviewed uses that address for RNG.

**Classification:** Replaced / protocol behavior changed.
**Significance:** Integrations expecting the former behavior may not be compatible. Actual impact depends on the contract's calls and deployment context. This is a source-level finding; a complete compatibility assessment requires deployed-call analysis and migration documentation.

## Expanded custom protocol functionality
The V2 source review identified custom functionality including HOST, Passkey, Shuffle, batch balance, Compound Interest, Trend, Merkle Proof, Batch Send, RNG and IBC-related functions. Each requires feature-specific source review, testing, and deployment verification. Presence in source does not establish that it is enabled in every deployment or safe for every use.

## Consensus and release evidence
The preserved review notes Clique/Shanghai-related changes and repeated fixes. Raw repository diff size is dominated by the upstream Geth foundation change and should not be presented as the size of Vitruveo-specific changes.

## V1 verification limitation
The V1 source repository currently returns 404 from this review environment. V1-side statements are retained from earlier research and should be treated as provisional until independently re-verified from accessible source.

## Evidence limits
Exact per-feature paths, line citations, tests, activation conditions and current deployment status remain to be attached to individual entries. The source commits above are the review baselines, not a claim about the latest deployed version.