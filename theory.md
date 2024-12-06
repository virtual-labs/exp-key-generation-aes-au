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
