Here are **clear, exam-ready 2-mark answers** for each question:

---

# 1. Encrypt "hello" using Caesar cipher with key = 3

Caesar cipher shifts each letter by 3 positions forward.

Plaintext: hello  
h → k  
e → h  
l → o  
l → o  
o → r

**Ciphertext: khoor**

---

# 2. Difference between conventional encryption and public key encryption

|Conventional Encryption|Public Key Encryption|
|---|---|
|Uses single key (same key for encryption and decryption)|Uses two keys (public and private keys)|
|Also called symmetric encryption|Also called asymmetric encryption|
|Faster|Slower|
|Example: AES, DES|Example: RSA|

---

# 3. Outline a HASH function with example

A hash function converts input data into a fixed-length output called a hash value.

Example:  
Input: hello  
Hash (SHA-256):  
2cf24dba5fb0a30e...

Hash is unique and cannot be reversed.

---

# 4. Define message digest

A message digest is a fixed-length hash value generated from a message using a hash function. It is used to verify data integrity.

Example:  
Message: hello  
Digest: 5d41402abc4b2a76b9719d911017c592

---

# 5. List five ingredients of a symmetric cipher

Five ingredients are:

1. Plaintext
    
2. Encryption algorithm
    
3. Secret key
    
4. Ciphertext
    
5. Decryption algorithm
    

---

# 6. Role of X.509 certificates in secure communications

X.509 certificates provide authentication by verifying the identity of users or servers. They contain public keys and are used in secure communications like HTTPS.

---

# 7. Main elements of an X.509 certificate

Main elements are:

1. Version number
    
2. Serial number
    
3. Issuer name
    
4. Subject name
    
5. Public key
    
6. Validity period
    
7. Digital signature
    

---

# 8. Importance of key distribution

Key distribution ensures that cryptographic keys are shared securely between sender and receiver. It prevents unauthorized access and ensures secure communication.

---

# 9. Four schemes for public key distribution

1. Public announcement
    
2. Public directory
    
3. Public key authority
    
4. Public key certificates
    

---

# 10. Countermeasures for replay attacks

Countermeasures include:

1. Use of timestamps
    
2. Use of nonces (random numbers)
    
3. Use of sequence numbers
    
4. Use of session tokens
    

---

If you want, I can also give these in **ultra-short format (1-line answers)** for faster exam writing.
Here are **clear, exam-ready 2-mark answers** for each question:

---

# 1. Encrypt “missclaretwiththeknifeinthelibrary” using Caesar cipher (key = 3)

Shift each letter by 3 forward:

m → p
i → l
s → v
s → v
c → f
l → o
a → d
r → u
e → h
t → w
w → z
i → l
t → w
h → k
t → w
h → k
e → h
k → n
n → q
i → l
f → i
e → h
i → l
n → q
t → w
h → k
e → h
l → o
i → l
b → e
r → u
a → d
r → u
y → b

**Ciphertext: plvvfoduhwzlwkwkhnqlihlqwkholeudub**

---

# 2. Does a digital signature ensure data integrity?

Yes. A digital signature ensures data integrity by using a hash function and private key encryption. If the message is modified, the signature verification fails.

---

# 3. Any two properties of hash function

1. Fixed output length
2. One-way function (cannot be reversed)

Other valid properties:

* Collision resistant
* Fast computation

---

# 4. Two general approaches to attacking a cipher

1. Cryptanalysis attack – attacker uses mathematical analysis
2. Brute force attack – attacker tries all possible keys

---

# 5. Compare symmetric and asymmetric encryption

| Symmetric Encryption         | Asymmetric Encryption        |
| ---------------------------- | ---------------------------- |
| Uses single key              | Uses public and private keys |
| Faster                       | Slower                       |
| Less secure key distribution | More secure key distribution |
| Example: AES                 | Example: RSA                 |

---

# 6. Define remote user authentication and its importance

Remote user authentication is the process of verifying the identity of a user accessing a system over a network.

Importance:

* Prevents unauthorized access
* Ensures secure communication

---

# 7. Countermeasures for replay attacks

1. Use timestamps
2. Use nonce values
3. Use sequence numbers
4. Use session keys

---

# 8. Note on Kerberos

Kerberos is a network authentication protocol that uses secret key cryptography and a trusted third party to authenticate users.

It uses:

* Authentication Server (AS)
* Ticket Granting Server (TGS)
* Tickets for secure authentication

---

# 9. Applications of X.509 certificates

1. HTTPS secure websites
2. Email security
3. Digital signatures
4. VPN authentication

---

# 10. Difference between Kerberos V4 and V5

| Kerberos V4                | Kerberos V5                        |
| -------------------------- | ---------------------------------- |
| Limited encryption support | Supports multiple encryption types |
| Fixed ticket lifetime      | Flexible ticket lifetime           |
| Less secure                | More secure                        |
| Limited functionality      | Improved functionality             |

---

If you want, I can also compile **all Units 1–5 important 2-mark questions with answers** for exam revision.
