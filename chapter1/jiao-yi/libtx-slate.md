```
//! Functions for building partial transactions to be passed
//! around during an interactive wallet exchange
```

#### ParticipantData

```
#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct ParticipantData {
    /// Id of participant in the transaction. (For now, 0=sender, 1=rec)
    pub id: u64,
    /// Public key corresponding to private blinding factor
    pub public_blind_excess: PublicKey,
    /// Public key corresponding to private nonce
    pub public_nonce: PublicKey,
    /// Public partial signature
    pub part_sig: Option<Signature>,
}
```

可以看出由两对公钥 + 签名构成。

#### Slate

```
/// A 'Slate' is passed around to all parties to build up all of the public
/// transaction data needed to create a finalized transaction. Callers can pass
/// the slate around by whatever means they choose, (but we can provide some
/// binary or JSON serialization helpers here).

#[derive(Serialize, Deserialize, Debug, Clone)]
pub struct Slate {
    /// The number of participants intended to take part in this transaction
    pub num_participants: usize, // 参与人数
    /// Unique transaction ID, selected by sender
    pub id: Uuid, // 唯一ID标识
    /// The core transaction data:
    /// inputs, outputs, kernels, kernel offset
    pub tx: Transaction, // 交易（关联对象）
    /// base amount (excluding fee)
    pub amount: u64, // 金额
    /// fee amount
    pub fee: u64, // 手续费
    /// Block height for the transaction
    pub height: u64, // 当前高度
    /// Lock height
    pub lock_height: u64, // 锁定高度
    /// Participant data, each participant in the transaction will
    /// insert their public data here. For now, 0 is sender and 1
    /// is receiver, though this will change for multi-party
    pub participant_data: Vec<ParticipantData>, // 参与人员数据
}
```

is\_complete

blank

add\_transaction\_elements

fill\_round\_1

fill\_round\_2

finalize

