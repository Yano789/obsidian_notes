Cryptography is the practice and study of techniques for secure communication in the presence of third parties called adversaries. It encompasses a wide range of methods for ensuring the **confidentiality**, **integrity**, **authenticity**, and **non-repudiation of data.**

The most basic way to support some of these security properties is via **encryption**. For example, encrypting your messages ensures confidentiality, as attackers are unable to understand your message / eavesdrop if good encryption algorithms are applied.

# How to Encrypt
Encrypting a simple text message is equivalent to _encrypting_ a number, which means that we can performing mathematical operations on those numbers.

The **ciphertext** (resulting encrypted value) will not be decodable anymore (which is the point!) until we decrypt them using the right _key_ (method). As a side note: encryption is **not** equivalent to encoding. Read this [appendix](https://natalieagus.github.io/50005/ns/04-network-security#cryptography-vs-encoding) section if you’d like to find out more.

## Substitution Cypher
A substitution cipher is a method of encryption where each unit of plaintext is replaced with ciphertext according to a fixed system.

A naive attempt to encrypt your text message is by mapping from a set of letters to another set as such:
![[Cryptography-1.webp]]

>[!MAIN DISADVANTAGE]
The **frequency** of the letters are not masked at all. Once you have deciphered some common letters, it is easy to fill in the gaps.

## Symmetric Key Cryptography
Symmetric key cryptography is a type of encryption where the same key is used for both encrypting and decrypting the data.
![[Cryptography-2.webp]]

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

![[Cryptography-4.webp]]

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

### Security of RSA
The security of RSA relies on the practical difficulty of factoring the product of two large prime numbers, the factoring problem. The larger the key size, the more secure the RSA system, although this also increases computational overhead. Common key lengths are 2048 and 4096 bits.

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

### Practical Uses
**Secure communications**: RSA can be used to encrypt data transmissions or to secure sensitive data by encrypting it with a public key, ensuring that only the holder of the private key can decrypt it. **Digital Signatures**: RSA is also used for digital signatures, where a message is signed with a sender’s private key and can be verified by anyone who has access to the sender’s public key.

Since public key $(n,e)$ is known to everybody and private key $(n,d)$ is only known to receiver, an attacker only need to guess the value of $d$

to decrypt the message: 
- $e$ is known and $d$ is related to $e$, $(ed−1)\ mod\ z=0$
- To find $z$, one has to know $p$ and $q$
- $p$ and $q$ is related to $n$, $n=p\times q$

Hence, one has to be able to perform **prime factorization** of n to guess p and q correctly. If n is sufficiently large, e.g: 1024 bits, it is hard to find the correct prime factors of n

(exponential complexity). To crack a simple 128-bit key, a supercomputer (in 2022) on estimate, requires ~10^(39) seconds. The universe is younger than that.

The **prime factorization** problem falls under [[Non-deterministic Polynomial Time (NP)]] Problem

RSA has stood the test of time, remaining robust against various attacks when correctly implemented and used with a sufficient key size. However, in the era of quantum computing, RSA’s security could potentially be compromised, leading to interest in developing quantum-resistant algorithms.

### Practical Issues

RSA requires exponentiation of very large numbers. This is computationally exhaustive. In comparison, DES is 100x faster than RSA.

One solution is to use [[Session Key]]

# Application Scenarios of Cryptography
## Case 1: Plain Message
![[Cryptography 1.webp]]

Suppose A would like to communicate with B via the internet. Without any cryptography features, an intruder T can send a fake message to B (claiming that it’s sent by A). There’s no way B can differentiate whether the message comes from T or the intended host A:

- Authentication is compromised
- Integrity is also compromised
- Confidentiality is also breached

## Case 2: Plain Message + IP Header
![[Cryptography-1 1.webp]]

In an attempt to prove A’s identity, A will send a message to B along with their IP. However without any encryption T knows A’s IP and will be able to craft a message with A’s IP and send it B. B won’t be able to differentiate whether the message comes from T or A:

- Authentication is compromised
- Integrity is also compromised
- Confidentiality is also breached

> [!Fun Fact]
> Faking one’s IP address like what T has done here is called **spoofing** 

## Case 3: Plain message + IP header + “secret” password
In yet another attempt to prove A’s identity, suppose A and B both share a secret codeword. A sends their IP + the secret codeword + message to B. Unfortunately, there’s nothing secret on the internet. An intruder T may **eavesdrop** on the conversation.

> [!Eavesdrop Attack]
> This attack involves eavesdropping the messages exchanged between A and B and use the information for malicious intent.

![[Cryptography-2 1.webp]]

T can echo back A’s IP + A’s “secret” password to B, but with a new message that does not come from A. Similarly, B cannot differentiate whether the message comes from A or T. Hence still without any form of encryption:

- Authentication is compromised
- Integrity is also compromised
- Confidentiality is also breached

>[!Note]
>To perform an **eavesdrop** attack, the attacker T does not even need to be in the same network. If the attacker is on the same local network as the target, it’s easier to perform packet sniffing because the attacker can directly intercept network traffic passing through the local network segment. This could be done by connecting to the same Wi-Fi network, being physically connected to the same Ethernet switch, or being on the same subnet. While being on the same network can _simplify_ eavesdropping attacks, attackers can still intercept communication remotely by targeting specific network nodes or exploiting **vulnerabilities** in network infrastructure. Head to [appendix](https://natalieagus.github.io/50005/ns/05-network-security-app#eavesdropping) if you’d like concreate examples on _how_ eavesdropping is done.

## Case 4: Encrypted message + encrypted password + IP header
>[!Note] In this scenario, Symmetric Key Cryptography is used since it’s faster than Asymmetric Key Cryptography.

![[Cryptography-3 1.webp]]

Now suppose both the message and “secret message” between A and B are now encrypted using symmetric key cryptography, such as 3DES. Even though now T cannot tell what the “secret message” between A and B is, nor can it read the content of the message. However, they can just **record** and **replay** or **playback** the cipher to B. This is called the replay/playback attack.

B is still not able tell if the incoming message + encrypted secret message comes from A or the intruder T. In this particular example, T does not get an extra $5000, but they damage B by incurring financial loss. The unauthorized duplicate transaction can disrupt legitimate financial transactions, cause financial losses for customers, and erode trust in the banking system and institutions involved.

>[!Playback/replay vs eavesdropping attack]
> Both replay attacks and eavesdropping attacks involve intercepting network communication.
> 
> Replay attacks involve **intercepting** and later re-**transmitting** captured network data to impersonate a legitimate user, while eavesdropping attacks involve passive interception of communication to extract sensitive information without altering it.
> 
> Replay attacks aim to **deceive** the target system by replaying captured data, whereas eavesdropping attacks focus on **listening** in on communication to extract confidential information.

Therefore in Case 4:

- Authentication is **not present** (due to replay/playback attack)
- Integrity is **present**: we know that A wrote the message at some point in time because only A has the symmetric key, just that it might **not** be right now (not live)
- Confidentiality is **present**: T cannot decipher the message, only replay it

>[!Important] Message Integrity _w/o_ Authentication?
> 
> Even if the message integrity is intact (in the case of replay attack), without authentication (signing of the message), there’s _no way_ to verify the timeliness or origin of the message (origin != author). The **significance** of message integrity without authentication does depend on the **context of the message**. An attacker can replay an old message, and while its content has not been altered (thus maintaining integrity), it could still cause **undesirable** effects because the recepient cannot distinguish it from a legitimate, authenticated message from the author.
> 
> For critical actions publication of software update, ensuring both integrity and authentication is essential to prevent that the software being installed indeed is published from reputable source (and not some malicious software).
> 
> However, integrity without authentication for non-critical message like **weather update** might be sufficient as the information is used for general awareness rather than critical decision making.

> [!Important] Message Integrity _with_ Authentication but _without_ Liveness?
> 
> In some scenarios that require **immediate** critical decision making, **liveness** is also an important requirement on top of **both** message integrity and authentication. For time-sensitive critical actions like transferring money and a live-voting system, ensuring integrity, authentication, **and** liveness is **essential** to prevent replay attacks and unauthorized duplicated actions.
> 
> It should be clear that the above examples of time-sensitive, critical decision-making scenarios (bank transfer, voting system) are _different_ from the **software update** and **weather update** scenarios aforementioned.

## Case 5: Signed message + Signed Nonce
>[!Note] In this scenario, Asymmetric Key Cryptography is used. Assume that confidentiality is not a requiremement (not critical)

Case 4’s issue is that it is susceptible to replay attack. To tackle this issue, B **wants** to authenticate A and ensure the **liveness** of A. That is, if A sends the message “Transfer me $5000”, B wants to make sure that it is indeed coming from A _right now_.

>[!Important] To do this, host A should **digitally sign** (encrypts with a private key) a 1-time generated number called **Nonce** (Number used only once).

![[Cryptography-4 1.webp]]

The scenario goes as follows:

- A generates a public-private key pair
- B would like to authenticate A (make sure that A is A), and so B sends Nonce N to A
    - Note: B to authenticate A, NOT the other way around
    - When B authenticates A, B is sure that A is live (and B is not communicating with some replayed / stale message)
- A then encrypts Nonce with their private key, producing a signed nonce
- A also encrypts the message with their private key, producing a signed message
- Then A sends the signed nonce along with A’s public key to B + signed message
- B verifies the Nonce using A’s public key, and check that it is indeed the Nonce N sent to A previously
    - This confirms that the message is **fresh** (not a replay message)
- B decrypts the signed message and acts upon it.
- B may send **confidential** message to A encrypting the reply message m with A’s public key. This way, only A can decipher the message.

There’s still one issue with this: there’s no way that B can tell that the public key belongs to A. This is susceptible to the man-in-the-middle attack (MITM). In other words, T is able to **hijack** the conversation between A and B

B’s intended “confidential” message to A is also susceptible to *Man-in-the-middle*:

![[Cryptography-5.webp]]


> [!Important] Man in the middle attack
> 
> In a Man-in-the-Middle (MITM) attack, an adversary intercepts communication between two parties, allowing them to **eavesdrop** on or **manipulate** the exchanged data. By impersonating one or both parties, the attacker can capture sensitive information and potentially alter the communication without detection.

Therefore in current Case 5:

- Authentication is **not present**: B does not know that A’s public key belong to A
- Integrity is **not present**: MITM attack allows T to pose as A to B and as B to A and tamper with the message exchanged
- Confidentiality is **not present**: same reason as above

There are **two solutions** to avoid the MITM attack: to utilise symmmetric key cryptography or to rely on [[Certificate Authority]] (CA).

### Utilise Symmetric Key Cryptography
This scenario can also be modified using symmetric key cryptography. Host A will encrypt the Nonce using a pre-established “shared key”. Upon receiving the message encrypted by a symmetric key that B knows only A has, B can confirm (to himself) that A wrote the message.

T can no longer hijack the conversation because simply it does not have the symmetric key. However, this solution requires A and B to both meet and share the key in person, so it is not exactly an ideal solution.

Let’s now review Case 5 again with the addition of CA:

![](https://natalieagus.github.io/50005/docs/NS/images/04-network-security/cse2024-case5c.drawio-4.png)

The addition of a CA enables B to be sure that A’s public key indeed belongs to A. However it is _still_ forcing A or B to encrypt messages with asymmetric key cryptography which is slow and takes up resources because it is computationally expensive. This improved Case 5 with a presence of a trusted CA nonetheless provides:

- **Authentication**: The Nonce ensures the message signed and sent by A is fresh. In other words, B authenticates A and ensures the liveness of A. The messages B received from A comes from A _right now_.
- **Confidentiality**: From B to A only, not the other way around.
    - This is because only A has CA-signed certificate. By encrypting messages using A’s verified public key, B ensures that only A can read the message.
    - If A would like to send a confidential message to B, then B needs to obtain CA-signed certificate too. A can then encrypt the message using B’s verified public key.
- **Integrity**: A has a CA **signed** certificate, hence B can verify that the signed message was authorized by A without alteration.

![](https://natalieagus.github.io/50005/docs/NS/images/04-network-security/cse2024-case5d.drawio-2.png)

## Case 6: Plain Message + Message Digest
In Case 5, we signed the _whole_ message using A’s private key to prove **integrity**, and we utilise Nonce (sent by B to A) so that B can **authenticate** A when A sign the Nonce. However recall that public-key encryption is costly, especially if the message is very large.

### Message Digest

> [!Important] Message Digest
> 
> A message digest, also known as a hash value or hash code, is a fixed-size alphanumeric string generated by applying a mathematical function (hash **function**) to an arbitrary amount of data. The purpose of a message digest is to uniquely represent the input data. Even a **tiny** change in the input data should result in a significantly different digest.

Message digests are commonly used in various security applications such as data integrity verification, digital signatures, and password storage. Popular hash functions include MD5, SHA-1, SHA-256, and SHA-3. However, due to vulnerabilities found in some older hash functions like MD5 and SHA-1, it’s recommended to use stronger algorithms like SHA-256 for security-sensitive applications.

These hash functions are of course publicly known, but it is a convenient and efficient way to transform long messages into **fixed**-length messages: small enough such that we can encrypt them using A’s private key without taking too much time.

![](https://natalieagus.github.io/50005/docs/NS/images/04-network-security/cse2024-case6.drawio.png)

We assume that Nonce and A’s CA-issued certificate verification were done beforehand (to establish authentication, where B authenticates A). Also, note that both A and B must use the **same** hash function. This can either be agreed a-priori, or specified in A’s CA issued certificate. Read this [appendix](https://natalieagus.github.io/50005/ns/05-network-security-app#chosen-hash-function) section to find out more.

To clarify, A sends the following after authentication is completed:

- Hashed message, encrypted with A’s private key
- Plain message (if confidentiality is not an issue)

B then confirms the **integrity** of the message:

- Hash the plaintext message
- Decrypt the encrypted hash sends by A using A’s public key
- Compare between (1) and (2) to ensure that A indeed sends the message

Therefore in Case 6:

- Authentication is **present**: We assume that nonce exchange as per Case 5 is already done and that A has CA-signed certificate
- Integrity is **present**: The signed message digest by A provides non-repudiation that the message was indeed written by A and not altered by any other party
- Confidentiality is **not required**: Since A sends the message to B in plain text, T can freely read the message.

Confidentiality is not always a security requirement, as it depends on the nature of the information being transmitted and the specific needs of the system or application. In some cases, confidentiality may not be a priority or may even be unnecessary, but **integrity** is necessary.

### Real-life scenario: Installer Download

A scenario where integrity is critical but _not_ confidentiality could be when downloading software updates from a trusted source, such as Microsoft official site. Imagine you’re downloading an update for your operating system directly from Microsoft’s official website. In this scenario:

1. **Integrity**: Ensuring the integrity of the downloaded file is crucial. You want to be certain that the file hasn’t been tampered with or altered in any way during transit. If the file’s integrity is compromised, it could potentially contain malware, viruses, or other harmful code that could compromise the security and stability of your system.
    
2. **Confidentiality**: Confidentiality is not important in this scenario as the installer is meant to be downloaded by any Windows user. This is unlike sensitive personal or financial information that you would like to download from a Banking site. In the Microsoft installer case, a long as the update process is transparent and the integrity of the update is guaranteed, the confidentiality of the update contents is not a primary concern.
    

By verifying the integrity of the file, you can trust that it hasn’t been tampered with and that it comes directly from the trusted source (e.g., Microsoft). This ensures the security and reliability of the update process without needing to protect the confidentiality of the update contents.

### Non Repudiation

The technique in Case 5 and 6 also supports non-repudiation: signing either the entire message _or_ the message digest with one’s private key.

> [!Important] Non repudiation
> 
> Non-repudiation is a property of cryptographic systems that ensures that a party cannot deny the authenticity of a digital signature or the integrity of a message that they have signed. In other words, if a party signs a message or document using their private key, they _cannot later claim that they did not sign it_ or that the message was _altered_ after they signed it.
> 
> B can then prove to the court that A wrote the message and no one else did.

>[!Caution]
>If A and B were to exchange messages using **symmetric key** cryptography only (assume that they have exchanged keys in person beforehand), will that support **non repudiation**?

### Hash Function Requirements

The hash function used to produce message digest **must** fulfil a certain criteria:

1. **Deterministic**: For a given input, the hash function always produces the same output. This property is crucial for ensuring consistency and predictability.
2. **Non-reversibility** (very important!): Hash functions are designed to be one-way functions, meaning it should be computationally infeasible to reverse the process and obtain the original input from the hash value. This property is crucial for maintaining the integrity and confidentiality of hashed data. This encompasses two properties:
    1. **Pre-image Resistance**: Given a hash value, it should be computationally infeasible to determine the original input data. This property ensures that the hash function protects the confidentiality of the input data.
    2. **Second Pre-image Resistance**: Given an input and its corresponding hash value, it should be computationally infeasible to find another input that produces the same hash value. This property ensures that the hash function maintains the integrity of the input data.
3. **Fixed Output Size**: The hash function generates a fixed-size output regardless of the size of the input. This property makes it easier to work with in various applications.
    
4. **Fast Computation**: Hash functions are designed to be computationally efficient, allowing them to process large amounts of data quickly. This efficiency is essential for real-time applications and systems with performance constraints.
5. **Collision Resistance**: It should be computationally infeasible to find two different inputs that produce the same hash value. This property ensures that the hash function can reliably distinguish between different inputs.
    
6. **Avalanche Effect**: A small change in the input data should result in a significantly different hash value. This property ensures that even minor alterations to the input data produce vastly different hash values, enhancing the security of the hash function.

These characteristics collectively make cryptographic hash functions like SHA-256 essential building blocks in various security protocols and cryptographic applications.

## Case 7: Secure Email

Both Case 5 and 6 ignores **confidentiality** as one of its security properties (simply not required). However, if communication between A and B **must** be secure, we need to find another way without fully utilising public key cryptography for the entire message exchanges. Recall that it is not realistic to encrypt lengthy messages using public-key cryptography. We can therefore use the public-key cryptography (+ digitally signed certificate by a trusted CA) to share a symmetric session key.

### Session Key

> [!Important] Session Key
> 
> A session key is a **temporary** encryption key used for securing communication between two parties during a single communication session or transaction. It’s typically generated dynamically for each session and discarded after the session ends, reducing the risk associated with long-term key exposure. This session key is typically symmetric.

Any party can initiate to share the session key first, **as long as the recipient you’re sending to has a public key (certified by CA)**. Here’s the general steps:

1. B has to obtain A’s public key from its CA-issued certicicate
2. B Generate a session key (e.g: using symmetric key cryptography)
3. B encrypts the session key to be sent back to A  
    By encrypting the session key with A’s public key, B is certain that only A can decrypt the session key (since A’s private key is owned by only A). Then, subsequent messages are encrypted using the session key.

This technique therefore provides for the following security features. Assume that **Nonce** verification (to authenticate that B and A are both live) is already done prior to the session:

- **Confidentiality**: message is encrypted by shared session key, that is typically valid only for one session. No intruder can decrypt the messages in realistic time.
- **Integrity**: not exactly, [depends on the type or format of data you’re sending, among other things](https://www.youtube.com/watch?v=tAdD5jp8knU). You might think that since the entire message is confidential (encrypted by session key), and can only be decrypted by the same session key, B or A should be certain that an intruder won’t be able to alter the message’s content on the fly. The hard part is knowing what’s the _true_ content.
    - Suppose B and A are just exchanging integers (bad protocol, yes but just using it as example), then if a malicious attacker randomly alters the bits, decryption by the symmetric key might result in an entirely new integer (not what the sender sent), and there’s no way for the receiver to know that that integer was sent by the sender.
    - Hence extra care must be taken to ensure integrity, one way is to utilise [Message Authentication Code](https://en.m.wikipedia.org/wiki/Message_authentication_code) or any protocol utilising one-way-functions.
- **Authentication**: A’s certificate is digitally signed by a trusted CA. This proves that A’s public key indeed belongs to A and therefore the session key shared by B can only be decrypted by A and no one else.

This technique alone does **not** support non repudiation: B cannot prove to the court that no one else but A wrote the message, because the symmetric key are owned by _both_ A and B. It is possible that B wrote a message posing as A and later “claim” that this message is written by A.

## Case 8: Secure email + non repudiation

If A needs to communicate securely with B and non-repudiation must be supported (e.g: prove that A’s messages are written by A), then A must provide a signed digest and encrypt both the message + encrypted hash together with the symmetric key:

Once B receives and decrypt the content: message + signed digest with the session key, B can:

1. Hash the received message
2. Decrypt the signed digest with CA-verified A’s public key
3. Compare the two hashes to confirm message integrity, i.e: the message is sent and written by A
4. If yes, this provides non-repudiation: the message is indeed sent by A (provable in court)

Three keys in total are utised to provide secure communication with non repudation: A’s public key, A’s private key, and Session Key.

![|721x287](https://natalieagus.github.io/50005/docs/NS/images/04-network-security/cse2024-case8.drawio-2.png)

>[!Important] 
>Non-repudiation in asymmetric cryptography relies on the sender’s private key, which is kept secret and known only to the sender. This prevents the sender from denying their involvement in signing the message. If non-repudiation is needed for both A and B, then both A and B must have a set of CA-verified public-private key pair.

