# Contract Review: Bridge and Token Control

This is a preliminary source-based summary of contract questions in preserved research. It is not a complete bytecode audit, fuzzing campaign, or formal verification.

## Administrative and upgrade authority
The reviewed bridge-token material identified roles including `DEFAULT_ADMIN_ROLE`, `UPGRADER_ROLE`, and `MESSAGE_OWNER`. Reported powers included upgrading the implementation, pausing transfers or bridging, blocking wallets, replacing bridge endpoints or messaging components, changing signer/fee settings, and recovering assets held by the contract.

**Risk:** Centralized administrative and upgrade trust.
**Verification needed:** current role-holder queries; multisig/timelock verification; proxy and implementation addresses; source/bytecode matching; historical upgrades. The presence of administrative powers does not itself demonstrate misuse.

## Bridge remainder/accounting logic
The preserved review described a bridge/burn path that rounds an amount to whole-token units and handles the remainder using the contract's token balance. It raised a possible accounting concern if contract-held remainder tokens can be returned without the caller supplying them.
**Status:** Requires deployed-version matching and a reproducible test. This is not a demonstrated drain.

## Recipient blocklist logic
The review flagged a bridge-unlock path in which the blocklist check appeared to apply to the authorized bridge caller rather than the destination recipient.
**Status:** Verify the exact deployed function, bytecode and recipient behavior before treating this as confirmed live impact.

## Supply reporting / ERC-20 integration
The research reported a nonstandard `totalSupply()` result potentially representing declared native-chain supply rather than bridged token supply, with a separate function tracking bridged supply.
**Potential significance:** Wallets, explorers, analytics and integrations may rely on standard ERC-20 `totalSupply()` semantics. Confirm the exact deployed implementation and integration effects.

## Proxy and implementation verification
A proxy's current implementation display is not a complete upgrade history. Record proxy and implementation addresses, verified source, bytecode match, upgrade events, role holders and dates.

## Limits
These are preserved research concerns, not proof of exploitation or intent. Current role holders, implementation, configuration and behavior have not been asserted as rechecked in this publication.