el # Documentation Source

Content pack for the public documentation site. Six pages total. Each section is
sized to render within the stated viewport budget on a 1440×900 viewport at the
site's default line-height (1.55) and base font size (15px).

Replace every `$PROJECT` with the final protocol name before publishing.
Zero vendor names are referenced: the privacy routing layer and the on-chain
swap aggregator are abstracted behind internal module names.

---

## 1. Introduction  ·  budget: 70vh

### What $PROJECT is

$PROJECT is a privacy layer for Solana that lets users move, swap, and distribute
SOL and major SPL tokens without exposing the graph between origin and
destination addresses. The product is delivered as a non-custodial web client
plus a small set of stateless HTTP services; no account, no KYC, no deposit
into a protocol pool.

### How it works at 1000ft

The client offers two execution modes per flow (send / swap / payroll):

- **Wallet mode.** The user signs a versioned transaction locally. For swaps
  the client builds the order against an on-chain liquidity aggregator; for
  transfers it assembles a `SystemProgram.transfer` (SOL) or a
  `TransferChecked` + idempotent ATA creation (SPL) instruction set. Nothing
  leaves the browser unsigned.
- **Private mode.** The client requests an ephemeral deposit address from the
  privacy routing layer, the user sends the input asset to that address, and
  the recipient receives the output asset on the same or a different chain.
  The direct on-chain link between sender and recipient is removed by the
  intermediate hop.

Both modes share the same UI surface; the difference is which module signs the
output transaction.

### What it is not

$PROJECT is not a shielded pool and does not produce zero-knowledge proofs.
It is a graph-break primitive: against passive chain analysis the source and
destination addresses are not directly linkable; against an adversary that
subpoenas the routing layer, linkability is recoverable. This tradeoff is
disclosed in-product every time a Private flow is initiated.

### Network support

Solana mainnet-beta only. Token-2022 mints are recognised for balance display.
Devnet and testnet are not exposed in the UI.

---

## 2. Features  ·  budget: 70vh

### Send

- SOL, USDC, USDT. Wallet mode signs a local transaction; Private mode routes
  through an ephemeral deposit address.
- Address validation is client-side (base58, 32–44 chars, `PublicKey` parse).
- Amount helpers: 25 / 50 / MAX are computed from the live on-chain balance
  with a 0.001 SOL fee reserve applied to native-SOL sends.
- Live status stepper for Private sends: waiting → confirming → exchanging
  → sending → finished, polled every 6s.

### Swap

- SOL → USDC / USDT.
- Wallet mode quotes against an on-chain aggregator, returns a versioned
  transaction, signs it locally, and executes via a stateless proxy.
- Private mode quotes the same pair through the routing layer, allowing a
  swap whose output address is unrelated to the input wallet.
- Slippage: Auto, 0.5 %, 1 %, 3 %, or custom (bps resolution).

### Payroll

- Up to 12 recipients per batch in Wallet mode. Each row is an ATA-idempotent
  instruction plus a `TransferChecked` against the payer's USDC / USDT ATA.
  One signature, one signed transaction, one solscan link on success.
- Private mode fans out to N independent exchanges and tracks each in the
  same stepper modal.
- Validation per row: address parse, positive amount, supported token.

### Balances

- On wallet connect the client issues a parallel `getBalance` +
  `getParsedTokenAccountsByOwner` across the classic Token and Token-2022
  programs. Results are normalised and displayed with three-decimal precision
  and trailing-zero trimming.
- Errors are surfaced in console under the `[balances]` tag for diagnosis.

### Compliance report

- One-click generator that scans the connected wallet's history and produces
  a record suitable for record-keeping or tax export. CSV and PDF export
  targets are stubbed behind the same entry point.

### Backup and restore

- The client generates a session keypair on first open, persisted in
  `localStorage` under `$PROJECT_session_key_v1`, and exposes it as a
  downloadable recovery file (`.txt`, address + raw secret, base64 encoded).
- Import restores a previously exported recovery file to the same slot.
- Verify balance reconciles local state against on-chain spent outputs.

### RPC

- Endpoint is driven by `NEXT_PUBLIC_SOLANA_RPC`. If unset, the client falls
  back to a public CORS-friendly node. The Solana Labs public endpoint is
  blocked client-side and is never used.

---

## 3. Our goal  ·  budget: 70vh

### Thesis

Financial privacy on a public chain is a product problem, not only a
cryptographic one. For the vast majority of users — freelancers invoicing in
stablecoins, teams running a payroll, traders rebalancing into a fresh
address — the threat model is passive surveillance and competitor analysis,
not nation-state forensics. A graph-break primitive solves that threat model
with one click and no lock-up.

### Design principles

1. **Non-custodial by default.** The browser signs everything that touches the
   user's wallet. The backend proxies network calls and never holds funds.
2. **Stateless services.** Every HTTP endpoint is stateless; rebooting the
   server loses no user state. The client is the source of truth.
3. **Disclosed tradeoffs.** Every Private flow shows the privacy model in the
   same modal where the deposit address is shown. No hidden assumptions.
4. **Zero config to first transaction.** Connect a standard Solana wallet,
   enter an address, press Continue. Nothing else is required.
5. **Failure is loud.** Quote failures, RPC errors, and routing errors surface
   on the same screen that caused them, with the machine-readable code shown
   below the human-readable message.

### Roadmap

- Batch sizes beyond 12 recipients via transaction splitting and lookup tables.
- Deterministic session-key derivation from the connected wallet signature,
  so the backup file becomes regenerable instead of stored.
- Optional native shielded-pool integration once a production-grade Solana
  primitive ships.
- SDK published as an npm package so third-party wallets can embed the
  send and swap flows.

---

## 4. Team  ·  budget: 50vh

### Engineering

A small team of engineers with prior work on Solana tooling, browser wallet
integrations, and high-throughput RPC infrastructure. We build in public
where possible and pick boring, well-understood primitives over novel
cryptography we cannot ourselves audit.

- **Protocol engineering** — transaction construction, swap routing,
  Token-2022 edge cases.
- **Client engineering** — React, wallet-adapter, GSAP-driven motion,
  accessibility, localisation.
- **Infrastructure** — stateless proxies, RPC pool, observability.
- **Research** — chain-analysis resistance modelling, threat-model
  documentation, audit coordination.

### Principles

We ship small. We write the threat model before the feature. We treat user
funds as uninsured and build accordingly. We do not own user state and we
do not want to.

### Contact

Public inbox for security disclosures is listed on the site footer. All
reports are triaged within 48 hours on business days.

---

## 5. Terms of service  ·  budget: 40vh

By using $PROJECT you agree to the following.

1. **No custody.** $PROJECT does not hold user funds at any point. Private
   flows route through a third-party routing layer that operates under its
   own terms; $PROJECT is not a party to that transfer.
2. **No financial advice.** The interface surfaces quotes and balances; it
   does not constitute investment, legal, or tax advice.
3. **No guarantees.** Transactions may fail due to network congestion, RPC
   degradation, slippage exceeding tolerance, or routing-layer capacity. The
   client reports failures; it does not compensate for them.
4. **Sanctions and jurisdiction.** The client is not available to users or
   addresses on sanctions lists published by OFAC, HMT, or the EU. Use where
   prohibited is at the user's own risk and is grounds for immediate
   termination of service access.
5. **Privacy model disclosure.** Private flows break the direct on-chain
   link between source and destination; they are not cryptographic mixers
   and do not protect against subpoena of the routing layer's logs.
6. **Changes.** These terms may change without individual notice. Continued
   use after a change constitutes acceptance.

---

## 6. Conditions of use  ·  budget: 40vh

1. **Wallet compatibility.** Phantom, Solflare, Backpack, and any other
   Wallet Standard-compliant Solana wallet. Hardware wallets are supported
   via their respective adapters.
2. **Minimums.** Private flows are subject to a routing-layer minimum that
   varies per asset and changes without notice. The client surfaces the
   minimum inline when an amount falls below it.
3. **Maximums.** Wallet-mode payroll is capped at 12 recipients per signed
   transaction to stay within the Solana 1232-byte transaction limit.
   Private-mode payroll has no per-batch cap but scales linearly in
   routing-layer calls.
4. **Slippage.** Default slippage tolerance is Auto; custom values are
   accepted at bps resolution. Swaps that exceed tolerance are rejected
   before the user signs.
5. **RPC usage.** Users supplying their own RPC endpoint via
   `NEXT_PUBLIC_SOLANA_RPC` are responsible for staying within their
   provider's rate limits.
6. **Backup responsibility.** The session key lives only in the user's
   browser. Clearing site data without first exporting the recovery file
   results in permanent loss of any session-scoped state. Funds custodied by
   the user's primary wallet are unaffected.

---

_End of content pack._
