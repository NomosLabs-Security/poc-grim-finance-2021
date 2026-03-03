# Grim Finance — Vault depositFor Reentrancy PoC

> **Educational Purpose Only** — This PoC is created for security research and education
> purposes only. It is a simplified simulation, not a fork replay against mainnet.

**Date:** 2021-12-19 | **Loss:** $30M | **Chain:** Fantom

## Quick Start
```bash
git clone https://github.com/NomosLabs-Security/poc-grim-finance-2021
cd poc-grim-finance-2021
forge install foundry-rs/forge-std --no-git
forge test -vvvv
```

## Vulnerability
The vault's `depositFor()` function used `safeTransferFrom` which triggered a callback to the recipient. A malicious token could re-enter `depositFor()` during this callback, inflating shares because the vault balance hadn't been updated yet.

## Key Contracts
- `src/Exploit.sol` — Vulnerable vault with depositFor reentrancy + fixed version
- `test/Exploit.t.sol` — Foundry test demonstrating the exploit

## License

MIT — For educational use only.
