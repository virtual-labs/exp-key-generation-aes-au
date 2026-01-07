### Theory

Key Expansion (Key Schedule):

Key Input: The original 128-bit key is divided into four words of 32 bits each.

Word Expansion:

Each word undergoes word expansion using a series of operations:
Substitution: Bytes are substituted using the AES S-box, a predefined 8-bit substitution table.
Rotation: Bytes in each word are rotated to the left.
Round Constant XOR: The first byte of the word is XORed with a round constant derived from Rijndael's Galois field.
This process is repeated until the key schedule generates the required number of round keys.
Round Key Generation:

The expanded key is divided into blocks of words, with each block forming a round key.
For AES-128, there are a total of 11 round keys (10 additional keys for the 10 rounds, plus the initial key).
Round Constants:

For each round, a round constant is used in the key expansion process. These round constants are predefined values derived from the mathematical constant Rijndael's Galois field.
Final Key Schedule:

The final key schedule is a matrix where each column represents a round key.
For AES-128, this matrix consists of 11 columns, each corresponding to a round key.
The key expansion process is crucial for the security of AES-128, ensuring that each round has a unique and independent key. The operations involved, such as substitution, rotation, and XOR with round constants, contribute to the overall complexity and strength of the encryption key.

---

### Theoretical Note:

The AES key generation process takes as input a 4-word (16-byte) key and produces a linear array of 44 words (156 bytes).

The following pseudo code describes the expansion:

```
KeyExpansion(byte key[16], word w[44]){
 Word temp;
 For(i=0;i<4;i++) w[i]=(key[4*i], key[4*i+1], key[4*i+2], key[4*i+3]);
 For(i=4;i<44;i++){
   Temp=w[i-1];
    If(I mod 4 = 0) temp = SubWord(RotWord(temp)) XOR Rcon[i/4];
    W[i]=w[i-4] XOR temp;
 }
}
```

• The key is copied into the 1st four words of the expanded key.

• The remainder of the expanded key is filled in four words at a time.

• Each added word w[i] depends on the immediately preceding word, w[i-1], and the word four positions back, w[i-4].

• In three out of four cases, a simple XOR is used.

• For a word whose position in the array w is a multiple of 4, a more complex function is used. Figure 5.6 illustrates the generation of the first eight words of the expanded key, using the symbol g to represent the complex function.

**The function g consists of the following subfunctions:**

1. **RotWord** performs a 1-byte circular left shift on a word. This means that an input word [b0, b1, b2, b3] is transformed into [b1, b2, b3, b0].

2. **SubWord** performs a byte substitution on each byte of its input word, using the S-box (Table 5.4a)

3. **Round Constant XOR:** The result of steps 1 and 2 is XORed with a round constant, Rcon[j]

**Round Constant:**

• The round constant is a word in which the three rightmost bytes are always 0.

• Thus, the effect of an XOR of a word with Rcon is to only perform an XOR on the leftmost byte of the word.

• The round constant is different for each round and is defined as Rcon[j]=(RC[j],0,0,0), with RC[1]=1, RC[j]=2 RC[j-1] and with multiplication defined over the field GF(2⁸).
