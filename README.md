# Apron Node

## Local Development

Follow these steps to prepare a local development environment :hammer_and_wrench:

### Setup Rust Environment
[https://substrate.dev/docs/en/knowledgebase/getting-started](https://substrate.dev/docs/en/knowledgebase/getting-started).


### Get Code
```
git clone -b upgrade_contract https://github.com/Apron-Network/apron-node.git
```

### Build

```bash
rustup default nightly-2021-11-08
rustup add target wasm32-unknown-unknown
cd apron-node
cargo build --release
```

### Run

Start a development chain:

```bash
./target/release/apron-node --dev
```

### Interact with node

By **Polkadot JS App**  
[https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#](https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#)

or

By **Canvas UI**

[https://paritytech.github.io/canvas-ui](https://paritytech.github.io/canvas-ui)
