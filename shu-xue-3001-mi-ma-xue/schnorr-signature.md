### Key generation

* Choose a private signing key,
  {\displaystyle x}
  ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4 "x")
  , from the allowed set.
* The public verification key is
  {\displaystyle y=g^{x}}
  ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/17b22b27d70b22f48d2a943d8a05c5fd5a32a095 "y=g^{x}") \# 公钥、
  .私钥

### Signing

To sign a message,{\displaystyle M}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/f82cade9898ced02fdd08712e5f0c0151758a0dd "M"): \# 原始消息

* Choose a random {\displaystyle k}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40 "k") from the allowed set.
* Let {\displaystyle r=g^{k}} ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/697f3df97cd0e1b124262f7f27684f43da3959a7 "r=g^{k}") \# 一次性公钥、
  .私钥
* Let {\displaystyle e=H\(r\parallel M\)}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/38dde48a22ba356e8ed549d28fb43d732f667a04 "{\displaystyle e=H\(r\parallel M\)}"), where{\displaystyle \parallel }![](https://wikimedia.org/api/rest_v1/media/math/render/svg/66ed42f2e3eab99383c61f27773eba258aefeaac "\parallel ")denotes concatenation and {\displaystyle r}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538 "r") is represented as a bit string. \# 加密结果
* Let {\displaystyle s=k-xe} ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/892b424a8a5f7e14c82ee68813ce8510a0769042 "{\displaystyle s=k-xe}") \# 签名结果

The signature is the pair,{\displaystyle \(s,e\)}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/0bf13ceb863a186059314683df30eec27cd9ff2b "{\displaystyle \(s,e\)}"). \# 最终签名

原始数据为 M

需要私钥 x, 一次性私钥 k

两个大的步骤：

1. 加密（动词）
2. 签名（动词）

结果由上述个步骤组两部分\(加密结果, 签名结果\)，称之为“签名（名词）”

### Verifying

* Let
  {\displaystyle r\_{v}=g^{s}y^{e}}
  ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/efe28cb691665238f37826576e40b4d60360bc67 "r\_{v}=g^{s}y^{e}")
* Let
  {\displaystyle e\_{v}=H\(r\_{v}\parallel M\)}
  ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/76d9ecdb41f28f61799fdf7151ed1da18e373100 "{\displaystyle e\_{v}=H\(r\_{v}\parallel M\)}")

If{\displaystyle e\_{v}=e}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/b435bf8daf143afe11896063ea6573a8749c4bf6 "e\_{v}=e")then the signature is verified.

验证：根据公钥、最终签名、原始消息能够重新计算出加密结果。

### Proof of correctness

It is relatively easy to see that{\displaystyle e\_{v}=e}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/b435bf8daf143afe11896063ea6573a8749c4bf6 "e\_{v}=e")if the signed message equals the verified message:

{\displaystyle r\_{v}=g^{s}y^{e}=g^{k-xe}g^{xe}=g^{k}=r}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/f935ad3fa54c3436d2406314571514afe5d5346c "r\_{v}=g^{s}y^{e}=g^{{k-xe}}g^{{xe}}=g^{k}=r"), and hence{\displaystyle e\_{v}=H\(r\_{v}\parallel M\)=H\(r\parallel M\)=e}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/f4b967799e69b1478ab53de05acc468f61e217e8 "{\displaystyle e\_{v}=H\(r\_{v}\parallel M\)=H\(r\parallel M\)=e}").

Public elements:{\displaystyle G}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/f5f3c8921a3b352de45446a6789b104458c9f90b "G"),{\displaystyle g}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/d3556280e66fe2c0d0140df20935a6f057381d77 "g"),{\displaystyle q}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/06809d64fa7c817ffc7e323f85997f783dbdf71d "q"),{\displaystyle y}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/b8a6208ec717213d4317e666f1ae872e00620a0d "y"),{\displaystyle s}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/01d131dfd7673938b947072a13a9744fe997e632 "s"),{\displaystyle e}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/cd253103f0876afc68ebead27a5aa9867d927467 "e"),{\displaystyle r}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538 "r"). Private elements:{\displaystyle k}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40 "k"),{\displaystyle x}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4 "x").

## EdDSA

门罗币实际使用的是 EdDSA

Edwards-curve Digital Signature Algorithm \(EdDSA\) is a digital signature scheme using a variant of Schnorr signature based on Twisted Edwards curves.

## 实际使用

We suppose we have the SHA256 hash function and the same G curve as above. In its simplest form, an aggregate signature is built from:

* the message`M`to sign, in our case the transaction fee
* a private key`x`, with its matching public key`x*G`
* a nonce`k`just used for the purpose of building the signature

We build the challenge`e = SHA256(M | k*G | x*G)`, and the scalar`s = k + e * x`. The full aggregate signature is then the pair`(s, k*G)`.

The signature can be checked using the public key`x*G`, re-calculating`e`using M and`k*G`from the 2nd part of the signature pair and by veryfying that`s`, the first part of the signature pair, verifies:

```
s*G = k*G + e * x*G
```

In this simple case of someone sending a transaction to a receiver they trust \(see later for the trustless case\), an aggregate signature can be directly built for a Grin transaction by calculating the total blinding factor of inputs and outputs`r`and using it as the private key`x`above. The resulting kernel is assembled from the aggregate signature generated using`r`and the public key`r*G`, and allows to verify non-inflation for all Grin transactions \(and signs the fees\).

Because these signatures are built simply from a scalar and a public key, they can be used to construct a variety of contracts using "simple" arithmetic.

## 步骤

公钥加密，私钥签名，最终签名。

