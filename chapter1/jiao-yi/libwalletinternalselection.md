#### selection

build\_send\_tx\_slate

```
/// Initialize a transaction on the sender side, returns a corresponding
/// libwallet transaction slate with the appropriate inputs selected,
/// and saves the private wallet identifiers of our selected outputs
/// into our transaction context
```

build\_recipient\_output\_with\_slate

```
/// Creates a new output in the wallet for the recipient,
/// returning the key of the fresh output and a closure
/// that actually performs the addition of the output to the
/// wallet
```

select\_send\_tx

```
/// Builds a transaction to send to someone from the HD seed associated with the
/// wallet and the amount to send. Handles reading through the wallet data file,
/// selecting outputs to spend and building the change.
```

inputs\_and\_change

```
/// Selects inputs and change for a transaction
```

select\_coins

```
/// Select spendable coins from a wallet.
/// Default strategy is to spend the maximum number of outputs (up to
/// max_outputs). Alternative strategy is to spend smallest outputs first
/// but only as many as necessary. When we introduce additional strategies
/// we should pass something other than a bool in.
/// TODO: Possibly move this into another trait to be owned by a wallet?
```



