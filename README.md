# scraptors

> Scraping + Tor + Rust: ergonomic, privacy‑preserving, and fingerprint‑aware network automation.

scraptors is an organization building a cohesive ecosystem of Rust crates and patch sets that enable high‑fidelity, low‑friction scraping over the Tor network while minimizing detectable TLS (JA3 / JA4) and HTTP/2 fingerprint surfaces.

## Fingerprint Evasion Strategy

We categorize surfaces:

1. TLS Layer
   - Control over: cipher suite ordering, ALPN list, GREASE usage, supported groups, signature algorithms, SNI timing.
   - Goal: Align with contemporary Tor Browser / mainstream Firefox/Chrome TLS profiles (configurable).
2. HTTP/2 Layer
   - Deterministic SETTINGS ordering / values.
   - Controlled initial window sizes and PRIORITY frames.
   - PseudoHeader configuration support.

| crate | origin | reason |
|-------|--------|--------|
| [scraptors/boring](https://github.com/scraptors/boring) | [cloudflare/boring](https://github.com/cloudflare/boring) | Patched BoringSSL with additional legacy fields. |
| [scraptors/h2](https://github.com/scraptors/h2) | [hyperium/h2](https://github.com/hyperium/h2) | SETTINGS, PRIORITY, and pseudo-header ordering. |
| [scraptors/hyper](https://github.com/scraptors/hyper) | [scraptors/hyper](https://github.com/hyperium/hyper) | Expose additional HTTP/2 APIs |
| [scraptors/hyper-util](https://github.com/scraptors/hyper-util) | [scraptors/hyper-util](https://github.com/hyperium/hyper-util) | Compatibility / convenience layer for hyper + h2. |

