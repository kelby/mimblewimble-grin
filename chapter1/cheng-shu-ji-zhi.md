Coinbase outputs \(block rewards & fees\) are "locked" and require 1,000 confirmations \(blocks added to the current chain\) before they mature sufficiently to be spendable.

## Timelocked Transactions

A transaction can be time-locked with a few simple modifications:

* the message`M`to sign becomes the block height`h`at which the transaction becomes spendable appended to the fee \(so`M = fee | h`\)
* the lock height`h`is included in the transaction kernel
* a block with a kernel that includes a lock height greater than the current block height is rejected



