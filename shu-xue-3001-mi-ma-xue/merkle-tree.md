In cryptography and computer science, a hash tree or Merkle tree is a tree in which every leaf node is labelled with the hash of a data block and every non-leaf node is labelled with the cryptographic hash of the labels of its child nodes. Hash trees allow efficient and secure verification of the contents of large data structures. Hash trees are a generalization of hash lists and hash chains.

## Merkle Mountain Ranges

Merkle Mountain Ranges are an alternative to Merkle trees.

#### Hashing and Bagging

Just like with Merkle trees, parent nodes in a MMR have for value the hash of their 2 children. Grin uses the Blake2b hash function throughout, and always prepends the node's position in the MMR before hashing to avoid collisions. So for a leaf`l`at index`n`storing data`D`\(in the case of an output, the data is its Pedersen commitment, for example\), we have:

```
Node(l) = Blake2b(n | D)
```

And for any parent`p`at index`m`:

```
Node(p) = Blake2b(m | Node(left_child(p)) | Node(right_child(p)))
```





