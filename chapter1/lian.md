**两部分：**

元数据

关联对象

## 元数据

db\_root String

head Tip

等

## 关联对象

store ChainStore

adapter ChainAdapter

orphans OrphanBlockPool

txhashset txhashset::TxHashSet

等

## 作用

“元数据”这部分不是很重要，主要是对其“关联对象”的处理。如：OrphanBlockPool、BlockContext、ChainStore、TxHashSet 等（注意：这里的部分概念仅是为了方便“链”进行管理，在其它模块，或者说在整个区块链上，意义不大）。

“链”是大脑、是协调者。协调下面的“软件”的多个模块，让它们协作起来。

