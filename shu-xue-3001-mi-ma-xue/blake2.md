运用哈希函数生成随机数

BLAKE and BLAKE2 are cryptographic hash functions based on Dan Bernstein's ChaCha stream cipher, but a permuted copy of the input block, XORed with some round constants, is added before each ChaCha round. Like SHA-2, there are two variants differing in the word size. ChaCha operates on a 4×4 array of words. BLAKE repeatedly combines an 8-word hash value with 16 message words, truncating the ChaCha result to obtain the next hash value. BLAKE-256 and BLAKE-224 use 32-bit words and produce digest sizes of 256 bits and 224 bits, respectively, while BLAKE-512 and BLAKE-384 use 64-bit words and produce digest sizes of 512 bits and 384 bits, respectively. When run on 64-bit x64 and ARM architectures, BLAKE2b is faster than SHA-3, SHA-2, SHA-1, and MD5.

