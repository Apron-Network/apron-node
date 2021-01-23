# Apron Node

## Local Development

Follow these steps to prepare a local development environment :hammer_and_wrench:

### Setup
[Rust development environment](https://substrate.dev/docs/en/knowledgebase/getting-started).


### Build

Build debug version

```bash
cd apron-node
cargo build
```

Build release version

```bash
cd apron-node
cargo build --release
```

## Run

### Development Chain

Purge any existing dev chain state:

```bash
./target/debug/apron-node purge-chain --dev
```

Start a dev chain:

```bash
./target/debug/apron-node --dev
```

Or, start a dev chain with detailed logging:

```bash
RUST_LOG=debug RUST_BACKTRACE=1 ./target/debug/apron-node -lruntime=debug --dev
```

### Use `release` version

Replace `debug` with `release`.

**Caution! Donot try to run `release` version everytime, it will take lots of time.**


### Using polkadot.js
Visit <https://polkadot.js.org/apps/?rpc=ws%3A%2F%2F127.0.0.1%3A9944#/settings/developer>

Fill the config in Settings>>Developer.
```js
{
  "Address": "<AccountId>",
  "LookupSource": "<AccountId>",
  "DataInfo": {
    "url": "Text",
    "data": "Text"
  }
}
```

#### Add OCW Signer
Run `./scripts/insert_alice_key.sh` to insert OCW signer. If the OCW signer does not have enough balance, please charge money as following instructions.
