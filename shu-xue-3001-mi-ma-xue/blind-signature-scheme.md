## Blind Signature

In cryptography, blinding is a technique by which an agent can provide a service to \(i.e., compute a function for\) a client in an encoded form without knowing either the real input or the real output.

* Suppose Alice wants Bob to sign a message **m**, but does not want Bob to know the contents of the message.
* Alice "blinds" the message **m**, with some random number **b** \(the blinding factor\). This results in **blind\(m,b\)**
* Bob signs this message, resulting in **sign\(blind\(m,b\),d\)**, where **d** is Bob's private key.
* Alice then unblinds the message using **b**, resulting in **unblind\(sign\(blind\(m,b\),d\),b\)**
* The functions are designed so that this reduces to **sign\(m,d\)**, i.e. Bob's signature on **m**

Alice 盲化因子：b

Alice 消息：m（不需要对外公布）

Bob 私钥：b

通用函数：blind、sign、unblind

Blind signature schemes can be implemented using a number of common public key signing schemes, for instance RSA and DSA. To perform such a signature, the message is first "blinded", typically by combining it in some way with a random "blinding factor". The blinded message is passed to a signer, who then signs it using a standard signing algorithm. The resulting message, along with the blinding factor, can be later verified against the signer's public key. In some blind signature schemes, such as RSA, it is even possible to remove the blinding factor from the signature before it is verified. In these schemes, the final output \(message/signature\) of the blind signature scheme is identical to that of the normal signing protocol.



