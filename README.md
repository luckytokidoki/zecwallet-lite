## Zingo PC apps

> WARNING! These apps are in active development. Some of the documentation below are aspirational until we finalize these for release. Do not use these apps with real money unless you specifically know what you are doing!

Zingo PC is a desktop light wallet client for Zcash. It has full support for all Zcash features:

- Send and receive transactions with [Unified Address](https://electriccoin.co/blog/unified-addresses-in-zcash-explained/)
- Send encrypted message with [shielded memo](https://electriccoin.co/blog/encrypted-memo-field/)

## Privacy Consideration

As a light wallet client, Zingo PC depends on [lightwalletd](https://github.com/zcash/lightwalletd) server which has some limitations that developers and users need to consider:

- While all the keys and transaction detection happens on the client, the server can learn which blocks contain your shielded transactions.
- The server also learns other metadata, including your IP address.
- Finally, note that t-addr doesn't provide privacy on-chain.

## Note Management

Zingo PC does automatic note and utxo management, which means it doesn't allow you to manually select which address to send outgoing transactions from. It follows these principles:

- Defaults to sending shielded notes from the same shielded pool when sending to a Unified Address or legacy shielded address
- Sapling and Orchard notes need at least 3 confirmations before they can be spent
- Can use ZEC from multiple shielded notes in the same transaction
- Will automatically move your transparent ZEC to the most modern shielded pool (currently [Orchard](https://zips.z.cash/zip-0224)) at the first opportunity
  - When sending ZEC to a Unified Address, Zingo PC will also use the transaction to additionally shield your transparent ZEC, i.e., send your transparent funds to your own Unified Address in the same transaction

## Getting Started

Zingo PC is built with Electron and can be build from source. It will also automatically compile the [Rust crates](https://github.com/zcash/librustzcash) needed to run a Zcash wallet.

### Prerequisites

Building Zecwallet Lite requires:

- [Nodejs v12.16.1 or higher](https://nodejs.org)
- [Yarn](https://yarnpkg.com)
- [Rust v1.40+](https://www.rust-lang.org/tools/install)
- [Electron](https://www.electronjs.org/)

### Build and Run Instructions

> The following instructions are tested on Ubuntu and Arch Linux:

```
git clone https://github.com/zingolabs/zingo-pc.git
cd zingo-pc

yarn install
yarn build
yarn start
```

You should see `Starting the development server...`
and then `Compiled successfully!` printed out in this terminal.

Then, in another terminal instance, run

```
electron .
```

Two windows should open, one for the app and one for debugging.
