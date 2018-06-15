## Dandelion in Grin: Privacy-Preserving Transaction Propagation

关键词：隐私保护。一石二鸟

1、隐藏 IP

Dandelion is a new transaction broadcasting mechanism that reduces the risk of eavesdroppers linking transactions to the source IP.

2、混币

Moreover, it allows Grin transactions to be aggregated \(removing input-output pairs\) before being broadcasted to the entire network giving an additional privacy perk.

## Mechanism

Dandelion transaction propagation proceeds in two phases: first the “stem” phase, and then “fluff” phase. During the stem phase, each node relays the transaction to a_single_peer. After a random number of hops along the stem, the transaction enters the fluff phase, which behaves just like ordinary flooding/diffusion. Even when an attacker can identify the location of the fluff phase, it is much more difficult to identify the source of the stem.

Illustration:

```
                                                   ┌-> F ...
                                           ┌-> D --┤
                                           |       └-> G ...
  A --[stem]--> B --[stem]--> C --[fluff]--┤
                                           |       ┌-> H ...
                                           └-> E --┤
                                                   └-> I ...
```

This mechanism also allows Grin transactions to be aggregated during the stem phase and then broadcasted to all the nodes on the network. This result in transaction aggregation and possibly cut-through \(thus removing spent outputs\) giving a significant privacy gain similar to a non-interactive coinjoin with cut-through.

## Specification

The Dandelion protocol is based on three mechanisms:

1. _Stem/fluff propagation._Dandelion transactions begin in “stem mode,” during which each node relays the transaction to a single randomly-chosen peer. With some fixed probability, the transaction transitions to “fluff” mode, after which it is relayed according to ordinary flooding/diffusion.

2. _Stem Mempool._During the stem phase, each stem node \(Alice\) stores the transaction in a transaction pool containing only stem transactions: the stempool. The content of the stempool is specific to each node and is non shareable. A stem transaction is removed from the stempool if:

   1. Alice receives it "normally" advertising the transaction as being in fluff mode.
   2. Alice receives a block containing this transaction meaning that the transaction was propagated and included in a block.

3. _Robust propagation._Privacy enhancements should not put transactions at risk of not propagating. To protect against failures \(either malicious or accidental\) where a stem node fails to relay a transaction \(thereby precluding the fluff phase\), each node starts a random timer upon receiving a transaction in stem phase. If the node does not receive any transaction message or block for that transaction before the timer expires, then the node diffuses the transaction normally.



