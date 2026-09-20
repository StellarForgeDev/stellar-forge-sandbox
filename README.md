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

The integration tests require contract WASM artifacts from the contracts
workspace. They fail closed when those artifacts are missing; a green test run
must therefore include the real artifact-backed execution checks. The sandbox
CI workflow provisions the pinned contracts workspace before running tests.

## Lint

```bash
cargo fmt --all -- --check
cargo clippy --workspace -- -D warnings
```

## License

MIT — see the main [Stellar-Forge](https://github.com/StellarForgeDev/stellar-forge)
repository for the full license text.
