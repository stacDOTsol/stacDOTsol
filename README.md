# staccDOTsol

Retrieval, micropayments, and the plumbing between them. Mostly Solana and Rust,
mostly things that had to work on mainnet before I'd write about them.

---

### openzoo — pay-per-call inference, no account

[`openzoo.fun`](https://openzoo.fun) · [`npm i openzoo`](https://www.npmjs.com/package/openzoo) · [openzoo](https://github.com/staccDOTsol/openzoo)

~435 models behind one OpenAI-compatible endpoint. No API key, no signup, no
subscription — each call settles over [x402](https://x402.accrue.fund) from a local
burner wallet, on Solana, Base, or Robinhood Chain. `npx openzoo` starts a proxy on
`localhost:8402/v1` and an MCP server; point Cursor or Claude Code at it and the
per-call payment is invisible.

The interesting part isn't the payments, it's what sits in front of the models.

### leCore — bind a corpus once, then ask it anything

[leCore](https://github.com/staccDOTsol/leCore) · [benches.openzoo.fun](https://benches.openzoo.fun)

Holographic memory as a retrieval layer. A document gets bound once; every later
question reads a few thousand tokens of it instead of re-sending the whole thing.
That turns "this corpus doesn't fit in the context window" into a pricing question
rather than an architecture one — and re-asking a bound corpus is close to free.

Benchmarks are published with their methodology and their failures. When a headline
number turned out to be wrong — a 41.5% figure that was really 32.7% under honest
conditions — the site says so, with the reproduction. A benchmark you can't falsify
isn't a benchmark.

### token-wrap++ — wrapped tokens that accrue

[token-wrap-](https://github.com/staccDOTsol/token-wrap-) *(GitHub ate the plusses)*

SPL's `token-wrap` is strictly 1:1 — a format shim between SPL and Token-2022, unable
to express reserves growing. This fork makes the wrapped mint a **share of a pool**
instead: `shares = assets · supply / reserves`. Token-2022's transfer-fee extension
withholds on transfer, harvest is permissionless, and burning the harvest drops supply
— so NAV rises with no custom fee logic at all.

Rewritten on [Pinocchio](https://github.com/anza-xyz/pinocchio) for compute budget.
Every rounding decision favours the pool, never the caller, because the other
direction is the classic ERC-4626 drain.

### anyquote — the ~2,700 curves nobody indexes

[`anyquote.fun`](https://anyquote.fun)

Every Meteora DBC bonding curve is priced in some quote mint. Of ~459,000 `PoolConfig`
accounts on mainnet, ~456,000 quote in SOL, USDC, or JUP. anyquote is a launchpad and
explorer for the rest — curves denominated in anything else. Discover, launch, trade,
and claim fees against an exotic quote, all from live on-chain state.

### openzoo, everywhere else

[iOS](https://github.com/staccDOTsol/openzoo-ios) · [Android](https://github.com/staccDOTsol/openzoo-android) · [Solana Seeker](https://github.com/staccDOTsol/openzoo-seeker) · [Play Solana PSG1](https://github.com/staccDOTsol/openzoo-psg1) · [Omarchy plugin](https://github.com/staccDOTsol/omarchy-openzoo-plugin)

Same gateway, five front doors — including one that indexes your own machine and
answers questions about it locally.

### ttfx

[ttfx](https://github.com/staccDOTsol/ttfx) — terminal text effects as a single static
binary. A parity-checked port, which mostly meant discovering how many ways there are
to emit ANSI that *looks* right and renders wrong.

---

**Currently:** making retrieval cheap enough that context windows stop being the
constraint, and micropayments boring enough that nobody notices they're paying.

<sub>Also at <a href="https://github.com/accruedotfund">@accruedotfund</a>.</sub>
