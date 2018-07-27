ServerStateInfo

```
/// Server state info collection struct, to be passed around into internals
/// and populated when required
#[derive(Clone)]
pub struct ServerStateInfo {
	/// whether we're in a state of waiting for peers at startup
	pub awaiting_peers: Arc<AtomicBool>,
	/// Stratum stats
	pub stratum_stats: Arc<RwLock<StratumStats>>,
}
```

ServerStats

```
/// Simpler thread-unaware version of above to be populated and returned to
/// consumers might be interested in, such as test results or UI
#[derive(Clone)]
pub struct ServerStats {
	/// Number of peers
	pub peer_count: u32,
	/// Chain head
	pub head: chain::Tip,
	/// sync header head
	pub header_head: chain::Tip,
	/// Whether we're currently syncing
	pub sync_status: SyncStatus,
	/// Whether we're awaiting peers
	pub awaiting_peers: bool,
	/// Handle to current stratum server stats
	pub stratum_stats: StratumStats,
	/// Peer stats
	pub peer_stats: Vec<PeerStats>,
	/// Difficulty calculation statistics
	pub diff_stats: DiffStats,
}
```

WorkerStats

```
/// Struct to return relevant information about stratum workers
#[derive(Clone, Serialize, Debug)]
pub struct WorkerStats {
	/// Unique ID for this worker
	pub id: String,
	/// whether stratum worker is currently connected
	pub is_connected: bool,
	/// Timestamp of most recent communication with this worker
	pub last_seen: SystemTime,
	/// pow difficulty this worker is using
	pub pow_difficulty: u64,
	/// number of valid shares submitted
	pub num_accepted: u64,
	/// number of invalid shares submitted
	pub num_rejected: u64,
	/// number of shares submitted too late
	pub num_stale: u64,
}
```

StratumStats

```
/// Struct to return relevant information about the stratum server
#[derive(Clone, Serialize, Debug)]
pub struct StratumStats {
	/// whether stratum server is enabled
	pub is_enabled: bool,
	/// whether stratum server is running
	pub is_running: bool,
	/// Number of connected workers
	pub num_workers: usize,
	/// what block height we're mining at
	pub block_height: u64,
	/// current network difficulty we're working on
	pub network_difficulty: u64,
	/// cuckoo size used for mining
	pub cuckoo_size: u16,
	/// Individual worker status
	pub worker_stats: Vec<WorkerStats>,
}
```

DiffStats

```
/// Stats on the last WINDOW blocks and the difficulty calculation
#[derive(Clone)]
pub struct DiffStats {
	/// latest height
	pub height: u64,
	/// Last WINDOW block data
	pub last_blocks: Vec<DiffBlock>,
	/// Average block time for last WINDOW blocks
	pub average_block_time: u64,
	/// Average WINDOW difficulty
	pub average_difficulty: u64,
	/// WINDOW size
	pub window_size: u64,
}
```

DiffBlock

```
/// Last n blocks for difficulty calculation purposes
#[derive(Clone, Debug)]
pub struct DiffBlock {
	/// Block number (can be negative for a new chain)
	pub block_number: i64,
	/// Block network difficulty
	pub difficulty: u64,
	/// Time block was found (epoch seconds)
	pub time: u64,
	/// Duration since previous block (epoch seconds)
	pub duration: u64,
}
```

PeerStats

```
/// Struct to return relevant information about peers
#[derive(Clone, Debug)]
pub struct PeerStats {
	/// Current state of peer
	pub state: String,
	/// Address
	pub addr: String,
	/// version running
	pub version: u32,
	/// difficulty repored by peer
	pub total_difficulty: u64,
	/// height reported by peer on ping
	pub height: u64,
	/// direction
	pub direction: String,
}
```



