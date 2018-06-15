“交易池”最终要关联到“交易”

## TransactionPool &gt; Pool &gt; PoolEntry &gt; Transaction

元数据+其它关联对象



#### TransactionPool

包含两种“池子”\(txpool 和 stempool，结构是一样的，作用略有不同\)

作用主要是管理它们



#### PoolEntry

主要包含“池子实例”\(PoolEntry\)

作用主要是管理它们

#### PoolEntry

除了自身一些数据外，主要是关联着“交易”

它是被管理者



