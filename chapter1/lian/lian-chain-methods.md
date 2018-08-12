#### 重要操作

init

```
    /// Initializes the blockchain and returns a new Chain instance. Does a
    /// check on the current chain head to make sure it exists and creates one
    /// based on the genesis block if necessary.
```

process\_block\_no\_orphans

```
    /// Attempt to add a new block to the chain. Returns the new chain tip if it
    /// has been added to the longest chain, None if it's added to an (as of
    /// now) orphan chain.
```

validate

```
    /// Validate the current chain state.
```

compact

```
    /// Triggers chain compaction, cleaning up some unnecessary historical
    /// information. We introduce a chain depth called horizon, which is
    /// typically in the range of a couple days. Before that horizon, this
    /// method will:
    ///
    /// * compact the MMRs data files and flushing the corresponding remove logs
    /// * delete old records from the k/v store (older blocks, indexes, etc.)
    ///
    /// This operation can be resource intensive and takes some time to execute.
    /// Meanwhile, the chain will not be able to accept new blocks. It should
    /// therefore be called judiciously.
```

txhashset\_read

```
    /// Provides a reading view into the current txhashset state as well as
    /// the required indexes for a consumer to rewind to a consistent state
    /// at the provided block hash.
```

txhashset\_write

```
    /// Writes a reading view on a txhashset state that's been provided to us.
    /// If we're willing to accept that new state, the data stream will be
    /// read as a zip file, unzipped and the resulting state files should be
    /// rewound to the provided indexes.
```

其它操作也很重要，只是篇幅有限，这里挑几个出来讲解。

