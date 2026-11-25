# V2 Source Evidence Notes (Pinned Review Commit)

This supplement records source-level observations from the V2 repository at commit
[`ba0ef28d9844b84cd114b638b541c241af33e345](https://github.com/Vitruveo/vitruveo-protocol/commit/ba0ef28d9844b84cd114b638b541c241af33e345).
These are code observations, not proof of deployment, exploitability, or intent.

## 1. Custom precompile surface

[`core/vm/precompile.go`](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile.go#L15-L29) lists custom addresses including HOST, Passkey, Shuffle, batch-balance, Compound Interest, Merkle, Batch Send, RNG, IBC, and Trend.

The dispatch code at [lines 31–74](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile.go#L31-L74) shows these address cases are wired to corresponding handlers. This confirms source inclusion/dispatch at the reviewed commit—not activation in every network or successful behavior under all conditions.

## 2. RNG / Shuffle security limitations

[`core/vm/precompile_random.go`](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile_random.go#L32-L89) derives entropy from chain context: parent hash, context randomness or a difficulty fallback, transaction origin, origin nonce, timestamp, chain ID, and optional salt, then applies repeated Keccak hashing.

The source's own comments explain that in Clique contexts where Random is nil, Difficulty is used as a fallback and may be predictable to a transaction sender. Hash rounds do not make predictable inputs unpredictable.

The plain RNG output path at [lines 92–144](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile_random.go#L92-L144) derives output words from that seed. Shuffle uses the same seed generation at [lines 147–215](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile_random.go#L147-L215).

**Practical conclusion:** the source describes pseudo-randomness derived from public consensus/transaction context. Do not treat the plain RNG or Shuffle path as a secure lottery, wagering, or adversarial-game randomness source without a separate analysis of the actual chain context and implementation. This is a source-based limitation, not a reproduced exploit.

## 3. HOST registry request and validator signature

[`core/vm/precompile_host.go`](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile_host.go#L57-L110) shows HOST reads a request from a configured registry contract via EVM StaticCall and uses the validator identity when a global validator key exists.

The handler extracts URL and request templates from registry return data at [lines 196–211](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile_host.go#L196-L211), signs the resulting body with the global validator key at [lines 213–227](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile_host.go#L213-L227), and starts webhook delivery asynchronously at [lines 228–232](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile_host.go#L228-L232).

**Review questions:** who can authorize registry entries; what URLs and headers are accepted; whether local/private network destinations and redirects are restricted; how validator signing authority is scoped; and whether webhook side effects are expected during simulated/reverted execution. These require configuration and runtime testing.

## 4. Webhook destination validation and retries

At the reviewed commit, the webhook delivery code checks that the URL is non-empty and begins with HTTP or HTTPS before making requests; see [the pinned HOST file](https://github.com/Vitruveo/vitruveo-protocol/blob/ba0ef28d9844b84cd114b638b541c241af33e345/core/vm/precompile_host.go#L325-L415). This source section does not show an explicit private-network/localhost destination denylist. The actual reachable destinations depend on host networking, registry controls, DNS, redirect behavior, and deployment configuration; no network exploit was reproduced.

The same source implements multiple retries with long backoff delays, so a validator can retain asynchronous webhook work for an extended period after a request. Exact retry limits and delays are visible in the pinned code. Their operational effect depends on request volume and deployment.

## 5. Limits and access to the V1 comparison source

The V2 source links above are pinned to the reviewed commit. The V1 repository link and commit were recorded in earlier research, but the repository is currently not publicly fetchable from this review environment (GitHub returned 404). Accordingly, this supplement does **not** independently re-verify V1 source or make additional V1-to-V2 claims. The historical comparison remains provisional until the V1 source is accessible or a sanitized, redistributable source snapshot with provenance is published.

