## Committed

Commitment 的求和。

```
/// Implemented by types that hold inputs and outputs (and kernels)
/// containing Pedersen commitments.
/// Handles the collection of the commitments as well as their
/// summing, taking potential explicit overages of fees into account.
```

#### verify\_kernel\_sums

```
    /// Verify the sum of the kernel excesses equals the
    /// sum of the outputs, taking into account both
    /// the kernel_offset and overage.
```

sum\_commitments

```
/// Gathers commitments and sum them.

/// Utility to sum positive and negative commitments, eliminating zero values
```

sum\_kernel\_excesses

```
/// Gather the kernel excesses and sum them.

/// Utility function to take sets of positive and negative kernel offsets as
/// blinding factors, convert them to private key filtering zero values and
/// summing all of them. Useful to build blocks.
```



