```
//! Utilities to check the status of all the outputs we have stored in
//! the wallet storage and update them.
```

#### updater

retrieve\_outputs

```
/// Retrieve all of the outputs (doesn't attempt to update from node)
```

retrieve\_txs

```
/// Retrieve all of the transaction entries, or a particular entry
```

refresh\_outputs

```
/// Refreshes the outputs in a wallet with the latest information
/// from a node
```

map\_wallet\_outputs

```
/// build a local map of wallet outputs keyed by commit
/// and a list of outputs we want to query the node for
```

cancel\_tx\_and\_outputs

```
/// Cancel transaction and associated outputs
```

apply\_api\_outputs

```
/// Apply refreshed API output data to the wallet
```

retrieve\_info

```
/// Retrieve summary info about the wallet
/// caller should refresh first if desired
```

build\_coinbase

```
/// Build a coinbase output and insert into wallet
```

receive\_coinbase

```
//TODO: Split up the output creation and the wallet insertion
/// Build a coinbase output and the corresponding kernel
```



