Control the Grin server

```
SUBCOMMANDS:
    help     Prints this message or the help of the given subcommand(s)
    run      Run the Grin server in this console
    start    Start the Grin server as a daemon
    stop     Stop the Grin server daemon
```

## Server

```rust
/// Grin server holding internal structures.
pub struct Server {
    /// server config
    pub config: ServerConfig,
    /// handle to our network server
    pub p2p: Arc<p2p::Server>,
    /// data store access
    pub chain: Arc<chain::Chain>,
    /// in-memory transaction pool
    tx_pool: Arc<RwLock<pool::TransactionPool<PoolToChainAdapter>>>,
    /// Whether we're currently syncing
    currently_syncing: Arc<AtomicBool>,
    /// To be passed around to collect stats and info
    state_info: ServerStateInfo,
    /// Stop flag
    stop: Arc<AtomicBool>,
}
```

```rust
use common::adapters::{ChainToPoolAndNetAdapter, NetToChainAdapter, PoolToChainAdapter,
                       PoolToNetAdapter};
use common::stats::{DiffBlock, DiffStats, PeerStats, ServerStateInfo, ServerStats};
use common::types::{Error, Seeding, ServerConfig, StratumServerConfig};
```

#### tui-rs

Build terminal user interfaces and dashboards using Rust.

tui-rs is a Rust library to build rich terminal user interfaces and dashboards. It is heavily inspired by the Javascript library blessed-contrib and the Go library termui.

#### Cursive

A Text User Interface library for the Rust programming language.

It allows you to build rich user interfaces for terminal applications.

#### dandelion\_monitor

```
/// A process to monitor transactions in the stempool.
/// With Dandelion, transaction can be broadcasted in stem or fluff phase.
/// When sent in stem phase, the transaction is relayed to only node: the
/// dandelion relay. In order to maintain reliability a timer is started for
/// each transaction sent in stem phase. This function will monitor the
/// stempool and test if the timer is expired for each transaction. In that case
/// the transaction will be sent in fluff phase (to multiple peers) instead of
/// sending only to the peer relay.

```

#### seed

```
//! Mining plugin manager, using the cuckoo-miner crate to provide
//! a mining worker implementation
```

#### Syncer

```
/// Starts the syncing loop, just spawns two threads that loop forever
```



