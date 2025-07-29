Cryptography is the practice and study of techniques for secure communication in the presence of third parties called adversaries. It encompasses a wide range of methods for ensuring the **confidentiality**, **integrity**, **authenticity**, and **non-repudiation of data.**

The most basic way to support some of these security properties is via **encryption**. For example, encrypting your messages ensures confidentiality, as attackers are unable to understand your message / eavesdrop if good encryption algorithms are applied.

# How to Encrypt
Encrypting a simple text message is equivalent to _encrypting_ a number, which means that we can performing mathematical operations on those numbers.

The **ciphertext** (resulting encrypted value) will not be decodable anymore (which is the point!) until we decrypt them using the right _key_ (method). As a side note: encryption is **not** equivalent to encoding. Read this [appendix](https://natalieagus.github.io/50005/ns/04-network-security#cryptography-vs-encoding) section if you’d like to find out more.

## Substitution Cypher
A substitution cipher is a method of encryption where each unit of plaintext is replaced with ciphertext according to a fixed system.

A naive attempt to encrypt your text message is by mapping from a set of letters to another set as such:
![[Cryptography-1.png]]

>[!MAIN DISADVANTAGE]
The **frequency** of the letters are not masked at all. Once you have deciphered some common letters, it is easy to fill in the gaps.

## Symmetric Key Cryptography
Symmetric key cryptography is a type of encryption where the same key is used for both encrypting and decrypting the data.
![[Cryptography-2.png]]

Sender and receiver can encrypt plain text and decrypt ciphertext with the same key. In short, any plaintext can be converted into bits (e.g: with UTF8 encoding, ASCII encoding, etc). We can segment our message into bits of X bytes in length, and then generate a K bits key, and perform arithmetic operations between the two.

There are two algorithms for symmetric key encryption: **DES** and **AES**.

### Data Encryption Standard (DES)
- An algorithm to perform symmetric key cryptography
- 56-bit symmetric key is used
- 64-bit plaintext input is required (padding may be needed). If input size is longer than 64 bits, they need to be chopped into blocks of 64 bits.
    - The final block that does not amount to 64 bits will need to be padded to form 64 bits.
    - There might be some protocol variant that add probabilistic padding for each block, but the details are out of this syllabus.
- 16 identical rounds of encryption to produce 64-bit encrypted output
- It was US encryption standard in 1993
- Can be decrypted using brute force in less than a day using modern computing power

**3DES**, also known as **Triple DES**, is an encryption algorithm that uses the Data Encryption Standard (DES) cipher algorithm three times to each data block. It was developed to provide a more secure alternative as DES became vulnerable to brute-force attacks due to its relatively **short** key length of 56 bits.

By applying the DES cipher three times to each data block, 3DES significantly increases the security of DES by extending the effective key length. The typical key length used in 3DES is 168 bits (three 56-bit DES keys), but it can also operate in modes that use two keys (112 bits total).

### Advanced Encryption Standard (AES)
- AES is better algorithm to perform symmetric key cryptography as opposed to 3DES
- 128, 192, or 256-bit symmetric key is used
- 128-bit plaintext input blocks are accepted
    - Similarly, padding is needed for blocks < 128 bits
- 10,12,14 rounds of encryption is performed to produce 128-bit encrypted output
- AES replaced DES in 2001,
- If a 128-bit key is used, brute force decryption will take 1 billion billion years (yes, double billions) even with a supercomputer
    - However it can take much faster with a Quantum computer

## Asymmetric Key Cryptography
Asymmetric key cryptography, also known as public key cryptography, is an encryption method that uses a pair of keys for secure communication: a public key, which can be shared with everyone, and a private key, which is kept secret by the owner.

This method enables not only secure encryption but also **digital signatures** and **key exchanges**

![[Cryptography-4.png]]

### Rivest–Shamir–Adleman (RSA)
one of the first public-key cryptosystems and is **widely used for secure data transmission**. Invented in 1977 by Ron Rivest, Adi Shamir, and Leonard Adleman, it remains an important element in digital security and is used in a variety of applications like SSL/TLS for securing websites and digital signatures

- Sender, receiver, do not need to pre-share secret key prior to communication
- Public encryption key known to all
- Private decryption key known only to receiver
- 1024 - 4096-bit asymmetric (public-private) key pair generated
- 1 round of encryption required
- Input/output size: depends on key size and padding

**The RSA fulfils two important requirements of Asymmetric Key Cryptography:**

1. Given the public key, it is impossible to compute the private key
    - This **ensures** the **security** of the cryptographic system. The public key can be widely distributed without compromising the private key.
    - The difficulty of deriving the private key from the public key is based on **hard** mathematical problems, such as factoring large prime numbers (RSA) or solving discrete logarithms (Elliptic Curve Cryptography).
2. Able to produce a public-private key **pair** such that,
    - `encrypt(message, public_key) = ciphertext` (**encryption**)
    - `decrypt(ciphertext, private_key) = message` (**decryption**)
    - This ensures that messages **encrypted** with the public key can only be **decrypted** with the corresponding private key, providing confidentiality.

Note that the opposite can also be done:

- `encrypt(message, private_key) = signed_ciphertext` (**signing**)
- `decrypt(signed_ciphertext, public key) = message` (**verification**)
- This ensures that a message **signed** with the private key can be **verified** by anyone with the public key, providing **authenticity** and **integrity**. _This operation is typically referred to as signing rather than encrypting with the private key, and verifying rather than decrypting with the public key._

### How RSA Works

RSA involves a set of algorithms for key generation, encryption, and decryption:

1. **Key Generation**:
    - **Choose two large prime numbers**, $p$ and $q$.
		- The prime numbers $p$ and $q$ are chosen such that when multiplied together, they yield a product $n$ with the desired key length.
		- For example, for a 2048-bit RSA key, each prime $p$ and $q$ would typically be around `1024` bits in size.
	- **Compute $n=p\times q$** 
		- The value $n$ is used as the modulus for both the public and private keys. Its length, usually expressed in bits, is the key length.
	- **Calculate $z=\phi(n)=(p−1)\times (q−1)$**
		- $\phi$ is known as **Euler’s totient function** (see [appendix](https://natalieagus.github.io/50005/ns/04-network-security#eulers-totient-function) for more details).
	- **Choose** an integer $e$ such that $1<e<z$** and $e$ is **[[Coprime]]** to $z$.
		- This $e$ will be the **public** exponent.
	- **Determine** $d$ as the modular multiplicative inverse of $e \ mod \ z$, that is solve $d$ such that $(ed)\ mod\ z=1$.
		- This can be calculated using the Extended Euclidean Algorithm (out of syllabus, see Appendix to find out more).
		- This $d$ is the **private** exponent.
2. **Public Key and Private Key**:
    - The **public key** is made of the pair $(n,\ e)$
    - The **private key** consists of $(n,\ d)$
3. **Encryption**:
    - Given a **plaintext** message $M$ the ciphertext $C$ is computed as $C=M^e\ mod\ n$, using the **public** key.
4. **Decryption**:
    - Using the **private** key, the original message $M$ is recovered by computing $M=C^d\ mod\ n$, using the **private** key.
5. **Signing**:
    - Using the **private** key, the digital signature $S$ is computed as $S=M^d\ mod\ n$, using the **private** key.
6. **Verification**:
    - To **verify** a given digital signature $S$, we can compute $M=S^e\ mod\ n$, using the **public** key.

Example:
https://natalieagus.github.io/50005/ns/04-network-security#a-simple-example

### Message Segmentation
Messages that are long will be separated into segments such that the size of these segments is less than $n$.

This segmentation ensures that the message can be encrypted and decrypted correctly using modular exponentiation modulo $n$

The typical approach is to break the message into **fixed-size blocks** and then encrypt each block individually using RSA encryption. The size of the blocks depends on the size of the modulus $n$ and the desired security level. You will know more about this during the lab and PA2.

For example, if you have a 2048-bit RSA key, the modulus $n$ would be a 2048-bit number. In this case, you would typically **break** the plaintext message into smaller blocks that are significantly smaller than 2048 bits, ensuring that each block is less than $n$ in value.

- After encrypting each block separately, you can **concatenate** the ciphertext blocks together to form the final encrypted message.
- During decryption, the same process is applied in reverse. Each ciphertext block is decrypted separately using modular exponentiation modulo $n$ and then the decrypted blocks are concatenated together to recover the original plaintext message.

Segmenting the message into smaller blocks ensures that RSA encryption and decryption can be performed efficiently and correctly, even for long messages.

### Conceptual Differences: Encryption vs Signing
**Encryption**: The primary goal is confidentiality. Encryption with a public key ensures that only the holder of the corresponding private key can decrypt and read the message. 

**Signing**: The primary goals are authenticity and integrity. Signing with a private key allows anyone with the public key to verify who sent the message and that it has not been altered.