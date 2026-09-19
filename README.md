# Stellar-Forge Sandbox Runner

Native Rust executable that loads a Soroban contract WASM into an in-process
Soroban `Env`, deploys it, and invokes requested functions. It is the execution
engine behind the Stellar-Forge Playground.

## Architecture

The Playground API route spawns the sandbox-runner via `execFile`, pipes a JSON
request over stdin, and parses the JSON response from stdout. The runner
compiles the contract in an isolated Soroban host, mocks constructor auth,
then enforces auth for each subsequent call via `mock_auths`. Results are
JSON-serialized ScVal values.

## Part of Stellar-Forge

This repository is a component of the [Stellar-Forge](https://github.com/StellarForgeDev/stellar-forge)
developer platform. It is consumed as a Git submodule by the
[stellar-forge-contracts](https://github.com/StellarForgeDev/stellar-forge-contracts)
repository.

## Build

```bash
cargo build --release
```

## Test

```bash
cargo test --workspace
```

Note: Some integration tests reference contract WASM artifacts from the parent
contracts workspace. These tests gracefully skip when the WASM files are not
present (e.g., in standalone builds or CI environments without the Stellar CLI).

## Lint

```bash
cargo fmt --all -- --check
cargo clippy --workspace -- -D warnings
```

## License

MIT — see the main [Stellar-Forge](https://github.com/StellarForgeDev/stellar-forge)
repository for the full license text.
