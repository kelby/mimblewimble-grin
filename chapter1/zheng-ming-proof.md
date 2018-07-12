## 如何挖矿成功？

Proof 与 Difficulty 比较：找到的数据，符合目标，即为成功。

相关概念：难度 Difficulty

    /// A Cuckoo Cycle proof of work, consisting of the shift to get the graph
    /// size (i.e. 31 for Cuckoo31 with a 2^31 or 1<<31 graph size) and the nonces
    /// of the graph solution. While being expressed as u64 for simplicity, each
    /// nonce is strictly less than half the cycle size (i.e. <2^30 for Cuckoo 31).
    ///
    /// The hash of the `Proof` is the hash of its packed nonces when serializing
    /// them at their exact bit size. The resulting bit sequence is padded to be
    /// byte-aligned.
    ///
    #[derive(Clone, PartialOrd, PartialEq)]
    pub struct Proof {
    	/// Power of 2 used for the size of the cuckoo graph
    	pub cuckoo_sizeshift: u8,
    	/// The nonces
    	pub nonces: Vec<u64>,
    }



