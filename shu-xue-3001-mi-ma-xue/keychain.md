## ExtKeychain

/// Implementation of the Keychain trait based on an extended key derivation scheme.

```
pub struct ExtKeychain {
    secp: Secp256k1,
    extkey: extkey::ExtendedKey,
    key_overrides: HashMap<Identifier, SecretKey>,
    key_derivation_cache: Arc<RwLock<HashMap<Identifier, u32>>>,
}
```

#### ExtendedKey

```
/// An ExtendedKey is a secret key which can be used to derive new
/// secret keys to blind the commitment of a transaction output.
/// To be usable, a secret key should have an amount assigned to it,
/// but when the key is derived, the amount is not known and must be
/// given.
#[derive(Debug, Clone)]
pub struct ExtendedKey {
    /// Child number of the extended key
    pub n_child: u32,
    /// Root key id
    pub root_key_id: Identifier,
    /// Key id
    pub key_id: Identifier,
    /// The secret key
    pub key: SecretKey,
    /// The chain code for the key derivation chain
    pub chain_code: [u8; 32],
}
```

## BlindSum

```
/// Accumulator to compute the sum of blinding factors. Keeps track of each
/// factor as well as the "sign" with which they should be combined.
#[derive(Clone, Debug, PartialEq)]
pub struct BlindSum {
    pub positive_key_ids: Vec<Identifier>,
    pub negative_key_ids: Vec<Identifier>,
    pub positive_blinding_factors: Vec<BlindingFactor>,
    pub negative_blinding_factors: Vec<BlindingFactor>,
}
```

#### Identifier

The Identifier is a /// semi-opaque structure \(just bytes\) to track keys within the Keychain.

```
pub struct Identifier([u8; IDENTIFIER_SIZE]);
```

#### BlindingFactor

随机数，混淆因子

BlindingFactor is a useful wrapper around a private key to help with /// commitment generation.

```
pub struct BlindingFactor([u8; SECRET_KEY_SIZE]);
```

#### Keychain

trait 接口，需实现方法：

from\_seed

from\_random\_seed

root\_key\_id

derive\_key\_id

derived\_key

commit

commit\_with\_key\_index

blind\_sum

sign

sign\_with\_blinding

secp



