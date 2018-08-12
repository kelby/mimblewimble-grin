#### Keychain

trait 接口，需实现方法：

from\_seed、from\_random\_seed

root\_key\_id、derive\_key\_id

derived\_key

commit、commit\_with\_key\_index

blind\_sum

sign、sign\_with\_blinding

secp

可用它生成各种密码学相关对象：

ExtKeychain

Identifier \*

SecretKey \*

Commitment \*

BlindingFactor \*

Signature \*

ChildKey

用到的密码学相关库：

rand 随机

blake2 散列哈希

secp 椭圆曲线 \*



