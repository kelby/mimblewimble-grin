An input or output value in a transaction can then be expressed as:

```
r*G + v*H

```

Where:

* _r _is a private key used as a blinding factor, _G _is an elliptic curve and their product`r*G`is the public key for _r _on _G_
* _v _is the value of an input or output and _H _is another elliptic curve.

Neither_v_nor_r_can be deduced, leveraging the fundamental properties of Elliptic Curve Cryptography.`r*G + v*H`is called a_Pedersen Commitment_.



