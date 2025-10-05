# scraptors

> Scraping + Tor + Rust = scraptors

scraptors is an organization building a cohesive ecosystem of Rust crates and patch sets that enable high‑fidelity, low‑friction scraping over the Tor network while minimizing detectable TLS (JA3 / JA4) and HTTP/2 fingerprint surfaces.

## Goal

Align with contemporary Tor Browser / mainstream Firefox/Chrome TLS profiles (configurable).

## Fingerprint Evasion Strategy

We categorize surfaces:

1. TLS Layer
   - Control over: cipher suite ordering, ALPN list, GREASE usage, supported groups, signature algorithms, SNI timing, ALPS.

2. HTTP/2 Layer
   - Deterministic SETTINGS ordering / values.
   - Expose additional upstreamed openssl APIs that are used by common browsers
   - Controlled initial window sizes and PRIORITY frames.
   - PseudoHeader configuration support.
   - kDHE, ffdhe2048, and ffdhe3072

| crate                                                                               | origin                                                                                                | reason                                                                                              |
| ----------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| [scraptors/arti-hyper-connector](https://github.com/scraptors/arti-hyper-connector) | n/a                                                                                                   | Core arti wrapper that allows simple access to tor                                                  |
| [scraptors/boring-util](https://github.com/scraptors/boring-util)                   | n/a                                                                                                   | Utility functions and traits that don't belong in cloudflare/boring                                 |
| [scraptors/boring](https://github.com/scraptors/boring)                             | [cloudflare/boring](https://github.com/cloudflare/boring)                                             | Patched BoringSSL with additional legacy fields.                                                    |
| [scraptors/boringssl](https://github.com/scraptors/boringssl)                       | [google/boringssl](https://github.com/google/boringssl/tree/478b28ab12f2001a03261624261fd041f5439706) | Patched branch for generating patches for [cloudflare/boring](https://github.com/cloudflare/boring) |
| [scraptors/h2](https://github.com/scraptors/h2)                                     | [hyperium/h2](https://github.com/hyperium/h2)                                                         | SETTINGS, PRIORITY, and pseudo-header ordering.                                                     |
| [scraptors/hyper](https://github.com/scraptors/hyper)                               | [scraptors/hyper](https://github.com/hyperium/hyper)                                                  | Expose additional HTTP/2 APIs                                                                       |
| [scraptors/hyper-util](https://github.com/scraptors/hyper-util)                     | [scraptors/hyper-util](https://github.com/hyperium/hyper-util)                                        | for hyper-util legacy Client                                                                        |
