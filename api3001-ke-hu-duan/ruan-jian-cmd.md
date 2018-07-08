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

## tui-rs

Build terminal user interfaces and dashboards using Rust.

tui-rs is a Rust library to build rich terminal user interfaces and dashboards. It is heavily inspired by the Javascript library blessed-contrib and the Go library termui.

## Cursive

A Text User Interface library for the Rust programming language.

It allows you to build rich user interfaces for terminal applications.



