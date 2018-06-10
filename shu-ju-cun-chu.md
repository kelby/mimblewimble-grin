\*\*grin\_chain store\*\*

相当于 ORM

The full state of a Grin chain consists of all the following data:

1. The full unspent output \(UTXO\) set.
2. The range proof for each output.
3. All the transaction kernels.
4. A MMR for each of the above \(with the exception that the output MMR includes hashes for _all _outputs, not only the unspent ones\).

  


