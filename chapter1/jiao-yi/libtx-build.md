```
//! Utility functions to build Grin transactions. Handles the blinding of
//! inputs and outputs, maintaining the sum of blinding factors, producing
//! the excess signature, etc.
//!
//! Each building function is a combinator that produces a function taking
//! a transaction a sum of blinding factors, to return another transaction
//! and sum. Combinators can then be chained and executed using the
//! _transaction_ function.
//!
//! Example:
//! build::transaction(vec![input_rand(75), output_rand(42), output_rand(32),
//!   with_fee(1)])
```

input

```
/// Adds an input with the provided value and blinding key to the transaction
/// being built.
```

coinbase\_input

```
/// Adds a coinbase input spending a coinbase output.
```

output

```
/// Adds an output with the provided value and key identifier from the
/// keychain.
```

with\_fee

```
/// Sets the fee on the transaction being built.
```

with\_lock\_height

```
/// Sets the lock_height on the transaction being built.
```

with\_excess

```
/// Adds a known excess value on the transaction being built. Usually used in
/// combination with the initial_tx function when a new transaction is built
/// by adding to a pre-existing one.
```

with\_offset

```
/// Sets a known tx "offset". Used in final step of tx construction.
```

initial\_tx

```
/// Sets an initial transaction to add to when building a new transaction.
/// We currently only support building a tx with a single kernel with
/// build::transaction()
```

partial\_transaction

```
/// Builds a new transaction by combining all the combinators provided in a
/// Vector. Transactions can either be built "from scratch" with a list of
/// inputs or outputs or from a pre-existing transaction that gets added to.
///
/// Example:
/// let (tx1, sum) = build::transaction(vec![input_rand(4), output_rand(1),
///   with_fee(1)], keychain).unwrap();
/// let (tx2, _) = build::transaction(vec![initial_tx(tx1), with_excess(sum),
///   output_rand(2)], keychain).unwrap();
///
```

transaction

```
/// Builds a complete transaction.
```

transaction\_with\_offset

```
/// Builds a complete transaction, splitting the key and
/// setting the excess, excess_sig and tx offset as necessary.
```



