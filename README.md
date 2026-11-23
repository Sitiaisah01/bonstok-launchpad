# Bonstok Token (BSTK)

A community token issued on the **Ammora** protocol's segmented bonding curve,
**GIWA Sepolia** (chain 91342) — built for the Ammora Builder Mission, Season 2.

**Live site:** https://sitiaisah01.github.io/bonstok-launchpad/

## On-chain record

| Item | Value |
| --- | --- |
| Token (BSTK, 9 decimals) | `0x7F8f74494B18fC25fF9Dd5105Fb370ca193EC7b8` |
| Bonding curve (ALC) | `0x72B8c21115522A76b5794f47E375CfE8d94E2D8e` |
| Team config | ID **87** · `0x70f07abeb53041b0a8630812971ae23601ed80ce18459589e013fb5d2596f448` |
| Creator / config owner | `0x0d5f67a80ce5eA5Ab29175938daA07b626E80f0B` |
| Quote token | WETH `0x4200000000000000000000000000000000000006` |
| Migration threshold | 0.05 WETH |
| First buy | 0.0005 WETH → 961,534.725971732 BSTK |

Transactions (GIWA Sepolia explorer):

- Wrap: `0x6e4dd42a33ee52dc929640772a8ff3c9df5146cfc7e007982412dea9a81dc75e`
- WETH approval: `0xf73b9791ec2fc831d0107fd55f9cf4f770342c7766246ece4d37d34d3cde6ca1`
- Atomic register + launch + first buy: `0xf56d4d5ada76366f59f7317ba790f05c5420cfe9427ce45e98344844bd416ec1`

## How it was built

A from-scratch TypeScript implementation on top of the public
`@ammora-protocol/sdk` (v0.3.9) and viem — no example code. The build:

1. Mirrors the economics of a proven team config (sale supply 1,000,000 BSTK,
   creator share 7,000 bps of non-protocol fees) with every role
   (owner / partner / liquidity / leftover) set to the creator wallet.
2. Wraps exactly 0.0005 ETH to WETH and approves the first-buy executor for
   exactly that amount.
3. Executes one atomic transaction: config registration + token launch +
   first buy, planned and simulated by the SDK's portable lifecycle planner.
4. Reconciles every receipt on-chain before proceeding; the curve is left
   **active and not graduated**.

The curve state after launch: status *Active*, quote reserve 0.000495 WETH
(first buy minus the 1% curve fee), canonical pool unset — trading happens on
the curve until the migration threshold is reached.

*Testnet demonstration project. Verify everything on the
[GIWA Sepolia explorer](https://sepolia-explorer.giwa.io).*
