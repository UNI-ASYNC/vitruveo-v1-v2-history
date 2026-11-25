# Carry-Forward Analysis: V1 → V2

This initial classification captures the transition areas identified in preserved research. It is not yet an exhaustive function-by-function inventory.

| V1 area | V2 status identified | Classification | Evidence / caveat |
|---|---|---|---|
| Geth client foundation (V1-era research identifies v1.13.0) | V2 based on Geth v1.13.15 | Modified / new foundation | Exact V1 version and commit need direct confirmation |
| Rebase precompile at `0x…FF` | RNG uses `0x…FF` in reviewed V2 source | Replaced | Source address/function change; compatibility depends on deployed calls |
| Clique consensus | Clique remains with newer client modifications | Preserved / modified | Activation and consensus behavior require detailed commit comparison |
| Custom precompile architecture | V2 includes broader custom protocol surface | Expanded / new | Feature-by-feature testing and deployment verification needed |
| HOST | V2 custom feature | New | Review raised HTTP, signing, side-effect and resource-control concerns; conditions and exploitability not fully reproduced |
| Batch Send | V2 custom feature | New | Review raised transfer-source authorization and static-call behavior questions; requires reproduction |
| RNG / Shuffle | V2 custom features | New | Review raised predictability/manipulation concerns; no reproduced attack claimed here |
| Public release/migration evidence | Complete release and migration details not located in the reviewed material | Unverified / documentation gap | Limited to the research scope and date; not proof that no documentation exists elsewhere |

## Classification
- **Preserved:** mechanism remains.
- **Modified:** remains with changed implementation or behavior.
- **Replaced:** a different mechanism takes its place.
- **Removed:** absent from reviewed V2 scope; do not infer from incomplete source sets.
- **New:** introduced in V2.
- **Unverified:** evidence insufficient to classify confidently.

Each entry should be expanded with exact file paths, line references, commits, tests, activation conditions and deployment checks.