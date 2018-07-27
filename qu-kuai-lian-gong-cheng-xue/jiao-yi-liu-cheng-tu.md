整个过程，发送方、接收方均需要两对私钥参与。

该过程，不是零交互的。

## 发送方初始化

1: Create Transaction \*\***UUID**\*\* \(for reference and maintaining correct state\)

2: Set \*\***lock\_height**\*\* for transaction kernel \(current chain height\)

3: Select \*\***inputs**\*\* using desired selection strategy

4: Create \*\***change\_output**\*\*

5: Select blinding factor for \*\***change\_output**\*\*

6: Calculate \*\***tx\_weight**\*\*: MAX\(-1 \* \*\***num\_inputs**\*\* + 4 \* \*\***num\_change\_outputs**\*\* + 1, 1\)

\(+1 covers a single output on the receiver's side\)

7: Calculate \*\***fee**\*\*:  \*\***tx\_weight**\*\* \* 1\_000\_000 nG

8: Calculate total blinding excess sum for all inputs and outputs \*\***xS**\*\* \(private scalar\) 由之前数据而来的私钥

9: Select a random nonce \*\***kS**\*\* \(private scalar\) 发送方随机数

10: Multiply \*\***xS**\*\* and \*\***kS**\*\* by generator G to create public curve points \*\***xSG**\*\* and \*\***kSG**\*\*

## 接收方初始化

1: Check fee against number of \*\***inputs**\*\*, \*\***change\_outputs**\*\* +1 \* \*\***receiver\_output**\*\*\)

2: Create \*\***receiver\_output**\*\*

3: Choose random blinding factor for \*\***receiver\_output**\*\* \*\***xR**\*\* \(private scalar\) 由之前数据而来的私钥

4: Calculate message \*\***M**\*\* = \*\***fee** \| **lock\_height** \*\* 要加密的消息

5: Choose random nonce \*\***kR**\*\* \(private scalar\) 接收方随机数

6: Multiply \*\***xR**\*\* and \*\***kR**\*\* by generator G to create public curve points \*\***xRG**\*\* and \*\***kRG**\*\*

7: Compute Schnorr challenge \*\***e**\*\* = Blake2\(\*\***M**\*\* \| \*\***kRG**\*\* + \*\***kSG**\*\*\) 利用随机公钥对消息加密

8: Compute Recipient Schnorr signature \*\***sR**\*\* = \*\***kR**\*\* + \*\***e**\*\* \* \*\***xR**\*\* \(接收方需要 Schnorr 签名\)

## 发送方确认

1: Calculate message \*\***M**\*\* = \*\***fee** \| **lock\_height** \*\* 要加密的消息

2: Compute Schnorr challenge \*\***e**\*\* = Blake2\(\*\***M**\*\* \| \*\***kRG**\*\* + \*\***kSG**\*\*\) 利用随机公钥对消息加密

3: Verify \*\*sR\*\* by verifying \*\***kRG**\*\* + \*\***e**\*\* \* \*\***xRG**\*\* = \*\***sRG**\*\* \(根据接收方初始化第 8 步很容易验证\)

4: Compute Sender Schnorr signature \*\***sS**\*\* = \*\***kS**\*\* + \*\***e**\*\* \* \*\***xS**\*\* \(发送方需要 Schnorr 签名\)

## 接收方确认

1: Verify \*\*sS\*\* by verifying \*\***kSG**\*\* + \*\***e**\*\* \* \*\***xSG**\*\* = \*\***sSG**\*\* \(根据发送方第 4 步很容易验证\)

2: Calculate final signature \*\***s**\*\* = \(\*\***sS**\*\*+\*\***sR**\*\*, \*\***kSG**\*\*+\*\***kRG**\*\*\) 最终签名由两个 Schnorr 签名和两个 nonce 公钥组成

3: Calculate public key for \*\***s**\*\*: \*\***xG**\*\* = \*\***xRG**\*\* + \*\***xSG**\*\* \(最终公钥，根据输出 commit + 输入 commit 而来\)

3: Verify \*\***s**\*\* against excess values in final transaction using \*\***xG**\*\*

4: Create Transaction Kernel Containing:

Signature \*\***s**\*\* \(对应 TxKernel 里的 excess\_sig\)

Public key \*\***xG**\*\* \(最终公钥，对应 TxKernel 里的 excess\)

\*\***fee**\*\*

\*\***lock\_height**\*\*

对比数学/密码学“Schnorr signature”里介绍的标准流程，可以发现公私钥、随机数、签名都是根据发送方、接收方成对出现的。

