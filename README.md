# Vitruveo V1 → V2
## Protocol Transition & Historical Technical Review

This repository examines the historical transition from Vitruveo V1 to V2 using public source repositories, recorded version history, contract materials, and dated blockchain observations. This is a substantive historical review—not an empty scaffold.

## Initial findings

- **Client foundation changed:** the reviewed V1-era source is associated with Geth v1.13.0; the V2 client is based on Geth v1.13.15 and has a separate repository history.
- **Protocol functionality changed:** V2 includes a wider custom precompile surface, including HOST, Batch Send, RNG, Shuffle and additional functions.
- **Rebase-to-RNG address change:** the review identified the former Rebase function at the `0x…FF` precompile address as replaced by RNG in V2 source. This is a protocol compatibility issue requiring migration documentation and contract-call analysis.
- **Bridge contract control:** preserved research identified upgrade/admin roles with powers over upgrades, pausing, configuration and recovery. Current role holders and deployed implementation must be checked before stating current status.
- **Bridge accounting questions:** the review flagged token remainder handling, recipient blocklist checks and nonstandard supply reporting. These are documented as concerns requiring deployed-version matching and reproducible tests—not as proven exploits.

## Review pages
- [Transition timeline](timeline/v1-to-v2-transition.md)
- [Protocol changes](protocol-changes/what-changed.md)
- [Contract review](contract-review/contracts-and-functionality.md)
- [Carry-forward analysis](carry-forward-analysis/preserved-modified-removed.md)
- [Evidence and methodology](evidence/sources-and-methodology.md)

## Pinned source references
- [V1-era repository](https://github.com/Vitruveo/vitruveo-protocol-dev)
- [V1-era reviewed commit](https://github.com/Vitruveo/vitruveo-protocol-dev/commit/c4d5b01cb5f039964bed2a0416110885ffafc37)
- [V2 repository](https://github.com/Vitruveo/vitruveo-protocol)
- [V2 reviewed commit ba0ef28d](https://github.com/Vitruveo/vitruveo-protocol/commit/ba0ef28d9844b84cd114b638b541c241af33e345)

## Limits
The review distinguishes source-confirmed behavior from live observations, reproduction, conditional risk and unverified questions. It is not a commissioned audit or formal verification. Historical RPC observations are not current deployment checks. Original captures, correspondence, working drafts and reconstructions remain in a separate private archive.