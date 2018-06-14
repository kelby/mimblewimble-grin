### Key generation

* Choose a private signing key,
  {\displaystyle x}
  ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/87f9e315fd7e2ba406057a97300593c4802b53e4 "x")
  , from the allowed set.
* The public verification key is
  {\displaystyle y=g^{x}}
  ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/17b22b27d70b22f48d2a943d8a05c5fd5a32a095 "y=g^{x}")
  .

### Signing

To sign a message,{\displaystyle M}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/f82cade9898ced02fdd08712e5f0c0151758a0dd "M"):

* Choose a random {\displaystyle k}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/c3c9a2c7b599b37105512c5d570edc034056dd40 "k") from the allowed set.
* Let {\displaystyle r=g^{k}} ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/697f3df97cd0e1b124262f7f27684f43da3959a7 "r=g^{k}")
  .
* Let {\displaystyle e=H\(r\parallel M\)}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/38dde48a22ba356e8ed549d28fb43d732f667a04 "{\displaystyle e=H\(r\parallel M\)}"), where{\displaystyle \parallel }![](https://wikimedia.org/api/rest_v1/media/math/render/svg/66ed42f2e3eab99383c61f27773eba258aefeaac "\parallel ")denotes concatenation and {\displaystyle r}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/0d1ecb613aa2984f0576f70f86650b7c2a132538 "r") is represented as a bit string.
* Let {\displaystyle s=k-xe} ![](https://wikimedia.org/api/rest_v1/media/math/render/svg/892b424a8a5f7e14c82ee68813ce8510a0769042 "{\displaystyle s=k-xe}")

The signature is the pair,{\displaystyle \(s,e\)}![](https://wikimedia.org/api/rest_v1/media/math/render/svg/0bf13ceb863a186059314683df30eec27cd9ff2b "{\displaystyle \(s,e\)}").

## EdDSA

门罗币实际使用的是 EdDSA

Edwards-curve Digital Signature Algorithm \(EdDSA\) is a digital signature scheme using a variant of Schnorr signature based on Twisted Edwards curves.



