# Vitruveo V1 → V2
## Protocol Transition & Historical Technical Review

This repository documents a source-based historical and technical examination of the transition from Vitruveo V1 to V2.

## Scope
The review compares available V1 and V2 materials to identify:
- functionality and mechanisms preserved;
- functionality modified or reimplemented;
- mechanisms replaced or removed;
- new functionality introduced in V2; and
- questions that remain unverified due to incomplete evidence.

The review covers protocol and contract source material, version history, public documentation, and blockchain records where relevant and available.

## Evidence standard
Each substantive claim should link to the exact source and identify a version, commit, date, contract address, or block reference as applicable. Findings distinguish source-confirmed behavior, live observations, reproduced results, potential consequences, and unverified claims. A source-level observation alone does not establish deployed behavior or exploitability.

## Classification
- **Preserved** — V1 mechanism or functionality remains in V2.
- **Modified** — functionality remains but implementation or behavior changed.
- **Replaced** — a V1 mechanism was replaced by another.
- **Removed** — absent from the reviewed V2 source or implementation scope.
- **New** — introduced in V2.
- **Unverified** — available evidence is insufficient to classify confidently.

## Review limitations
This is an independent public-source historical review, not a commissioned security audit, formal verification, or assertion that every deployment uses the reviewed source. Unless a finding says otherwise, exploitability and production impact have not been established.

## Contents
- [Transition timeline](timeline/v1-to-v2-transition.md)
- [Protocol changes](protocol-changes/what-changed.md)
- [Contract review](contract-review/contracts-and-functionality.md)
- [Carry-forward analysis](carry-forward-analysis/preserved-modified-removed.md)
- [Sources and methodology](evidence/sources-and-methodology.md)

Only material necessary to substantiate the public comparison belongs here. Original source captures, private correspondence, drafts, working notes, reconstructions, and investigative archive material are maintained separately.
