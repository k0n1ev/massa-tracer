# 🌿 Massa Deep Origin Tracer

**A powerful, client-side recursive tracing tool for the Massa Blockchain.**

Massa uses a high-performance **account-based model**. To keep the network lightweight and blazing fast, standard Massa nodes only store a wallet's *current balance* and actively prune historical transactions. 

Because of this, tracing the true origin of funds becomes incredibly difficult once a user starts interacting with dozens of DeFi smart contracts, decentralized exchanges, or intermediary wallets. 

The **Massa Deep Origin Tracer** solves this by hooking into historical explorer APIs and recursively walking backward through the blockchain's history to calculate exactly where a wallet's current balance originally came from.

## ✨ Features

* **Proportional Origin Math:** Calculates the exact origins of a wallet's current Liquid MAS + Active Rolls by weighting historical inflows against the current balance.
* **DeFi Noise Filtering:** Ignores outgoing smart contract calls, failed roll buys, and DEX swaps that obfuscate a user's transaction history. It zeroes in entirely on incoming MAS transfers.
* **Recursive Tree Mapping:** Visually maps direct sources, intermediary hops, and specific origin dates in a clean, expandable UI tree.
* **Deep Pagination Engine:** Automatically bypasses rate limits and deeply paginates API requests in the background (scanning up to ~500 transactions deep for root wallets).
* **Interactive Ledger:** Includes a fully interactive, chronologically sorted "Recent Transfers" table with Incoming/Outgoing filters and local pagination.
* **Zero-Setup:** 100% client-side HTML, Tailwind CSS, and vanilla JavaScript. No local databases, no Python backends, no Node.js servers required.

## ⚙️ How It Works

1. **Balance Check:** Queries the official public mainnet RPC (`mainnet.massa.net/api/v2`) to get the exact current Liquid Balance and Roll Count.
2. **History Scraping:** Hits the Massexplo indexer API (using a seamless proxy fallback to bypass Cloudflare bot-protection) to extract raw historical operations.
3. **Recursive Math:** If a wallet has 20 MAS left, but received 100k MAS from MEXC and 100k MAS from Bitget historically, the engine proportionally splits the remaining 20 MAS as `50% MEXC / 50% Bitget` and stops tracing. If the funds came from an unknown wallet, it recursively dives into *that* wallet's history until it hits a known entity, a depth limit, or a genesis/staking gap.

## 🚀 Usage

Because the Massa Tracer is completely serverless, there is nothing to build or compile. 

1. Clone or download this repository.
2. Double-click `index.html` to open it in any modern web browser.
3. Paste a Massa address (`AU...` or `AS...`) and click **Trace Balance**.

*Alternatively, you can host this repository directly on GitHub Pages for free.*

## 🙏 Credits & Acknowledgements

This tool relies heavily on the massive historical databases maintained by the community. 
Huge thanks to the team at **[Massexplo.com](https://massexplo.com)** for providing the robust, open API infrastructure that powers the historical data in this application!

---
*If you find this tool helpful for your on-chain analysis, consider supporting the project:*
**Donate:** `AU121u5BvwhAofoBtU5MYNVntmHmnNxGy9Y897uhEwEbeY9v6CgXg`