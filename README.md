# adam-test

Public sandbox repository for testing the AutoMaintainer flow without touching the main `adam` repository.

## What this repo is for

This repository exists so contributors can test the full automation loop in a safe place:

1. Open an issue in `Gutslabs/adam-test`.
2. AutoMaintainer prices the issue and comments with the current fixed bounty.
3. Open a pull request that references the issue and includes an EVM wallet address.
4. AutoMaintainer reviews the diff, runs sandbox validation, and decides whether the PR is safe.
5. If the PR passes review and tests, AutoMaintainer merges it and sends the bounty payout from the demo treasury.

The main `Gutslabs/adam` repository is not used for these auto-merge and auto-payout tests.

This README pull request is also the live integration test for that flow.

## Current demo rules

- Issue pricing still uses the configured low-cost OpenRouter model for triage.
- Actual demo payout is fixed at `0.5 USDC` per accepted PR.
- Sandbox validation runs `bun install` and `bun test`.
- Payouts are sent on `Base Sepolia`.

## PR format

Use a pull request body like this:

```text
Fixes #1
Wallet: 0x66479e12FD7524DEB1f14164b0006A8fDb022B1f
```

`Fixes #...` links the PR to the priced issue. `Wallet: 0x...` tells AutoMaintainer where to send the payout after merge.

## Why there is a Bun test here

This repository includes a tiny Bun smoke test on purpose. That gives the E2B sandbox a real `bun install` and `bun test` flow to run, even for documentation-only pull requests.
