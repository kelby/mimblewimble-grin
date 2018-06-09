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

