# 🔐 Cryptography & Network Security
### Unit: Modular Arithmetic | Classical Encryption | Symmetric Ciphers

---

> **Study Tip:** These notes cover — Modular Arithmetic, Euclidean Algorithm, Fermat's & Euler's Theorem, Classic Encryption, Symmetric Cipher Model, Playfair Cipher, Hill Cipher.

---

## 📌 Table of Contents

1. [Modular Arithmetic](#1-modular-arithmetic)
2. [Euclidean Algorithm (GCD)](#2-euclidean-algorithm)
3. [Extended Euclidean Algorithm](#3-extended-euclidean-algorithm)
4. [Fermat's Little Theorem](#4-fermats-little-theorem)
5. [Euler's Theorem & Totient Function](#5-eulers-theorem--totient-function)
6. [Classic Encryption Techniques](#6-classic-encryption-techniques)
7. [Symmetric Cipher Model](#7-symmetric-cipher-model)
8. [Playfair Cipher](#8-playfair-cipher)
9. [Hill Cipher](#9-hill-cipher)
10. [Previous Year Questions Solved](#10-previous-year-questions-solved)

---

## 1. Modular Arithmetic

### What is Modular Arithmetic?

Modular arithmetic is a system of arithmetic for integers where numbers "wrap around" after reaching a certain value called the **modulus**.

```
a mod n = r
where r is the remainder when a is divided by n
0 ≤ r < n
```

### Key Properties

| Property | Formula |
|----------|---------|
| **Commutativity** | (a + b) mod n = (b + a) mod n |
| **Associativity** | [(a + b) + c] mod n = [a + (b + c)] mod n |
| **Distributivity** | [a(b + c)] mod n = [(ab + ac)] mod n |
| **Additive Inverse** | (a + (-a)) mod n = 0 |

### Modular Addition & Multiplication

```
(a + b) mod n = [(a mod n) + (b mod n)] mod n
(a × b) mod n = [(a mod n) × (b mod n)] mod n
(a - b) mod n = [(a mod n) - (b mod n)] mod n
```

### Example Problems

**Example 1:** Compute (11 + 8) mod 7
```
(11 + 8) mod 7 = 19 mod 7 = 5
OR
(11 mod 7 + 8 mod 7) mod 7 = (4 + 1) mod 7 = 5 ✓
```

**Example 2:** Compute (7 × 15) mod 11
```
(7 × 15) mod 11 = 105 mod 11 = 6
OR
(7 mod 11 × 15 mod 11) mod 11 = (7 × 4) mod 11 = 28 mod 11 = 6 ✓
```

**Example 3:** Find the additive inverse of 5 mod 11
```
5 + x ≡ 0 (mod 11)
x = 6  →  5 + 6 = 11 ≡ 0 (mod 11) ✓
```

**Example 4:** Find the multiplicative inverse of 5 mod 11
```
5 × x ≡ 1 (mod 11)
5 × 9 = 45 = 4×11 + 1 ≡ 1 (mod 11)
∴ Multiplicative inverse of 5 mod 11 = 9
```

### Modular Exponentiation

Used to compute a^b mod n efficiently.

**Fast Exponentiation (Square and Multiply):**

To compute 7^11 mod 13:
```
11 in binary = 1011

Start: result = 1, base = 7

bit 1 (LSB): result = 1 × 7 = 7,    base = 7² mod 13 = 49 mod 13 = 10
bit 1:        result = 7 × 10 = 70 mod 13 = 5,  base = 10² mod 13 = 100 mod 13 = 9
bit 0:        result = 5 (no multiply), base = 9² mod 13 = 81 mod 13 = 3
bit 1 (MSB): result = 5 × 3 = 15 mod 13 = 2

∴ 7^11 mod 13 = 2
```

### Congruence

Two integers a and b are **congruent modulo n** if n divides (a - b):
```
a ≡ b (mod n)  ←→  n | (a - b)
```

**Example:** 23 ≡ 2 (mod 7) because 7 | (23 - 2) = 21

---

## 2. Euclidean Algorithm

### Greatest Common Divisor (GCD)

The **GCD** of two integers is the largest integer that divides both.

**Theorem:** gcd(a, b) = gcd(b, a mod b)

### Algorithm

```
EUCLIDEAN GCD(a, b):
    while b ≠ 0:
        r = a mod b
        a = b
        b = r
    return a
```

### Diagram

```
gcd(a, b)
    │
    ▼
 Is b = 0?
    │
   YES──────► return a
    │
    NO
    │
    ▼
 r = a mod b
 a = b
 b = r
    │
    └──────► repeat
```

### Example 1: gcd(72, 56)

| Step | a | b | r = a mod b |
|------|---|---|-------------|
| 1 | 72 | 56 | 16 |
| 2 | 56 | 16 | 8 |
| 3 | 16 | 8 | 0 |
| 4 | 8 | 0 | — |

**∴ gcd(72, 56) = 8**

### Example 2: gcd(1160718174, 316258250)

```
gcd(1160718174, 316258250)
= gcd(316258250, 211943424)
= gcd(211943424, 104314826)
= gcd(104314826, 3313772)
= gcd(3313772, 1238)
= gcd(1238, 1066)
= gcd(1066, 172)
= gcd(172, 26)
= gcd(26, 16)
= gcd(16, 10)
= gcd(10, 6)
= gcd(6, 4)
= gcd(4, 2)
= gcd(2, 0)
= 2
```

### Example 3: gcd(100, 75)

```
gcd(100, 75):
100 = 1 × 75 + 25
 75 = 3 × 25 + 0
∴ gcd(100, 75) = 25
```

---

## 3. Extended Euclidean Algorithm

The Extended Euclidean Algorithm finds integers x and y such that:

```
ax + by = gcd(a, b)
```

This is used to find **multiplicative inverses** in modular arithmetic.

### Algorithm

```
EXTENDED_GCD(a, b):
    if b == 0:
        return (a, 1, 0)   → gcd, x, y
    else:
        (g, x1, y1) = EXTENDED_GCD(b, a mod b)
        x = y1
        y = x1 - (a // b) * y1
        return (g, x, y)
```

### Example: Find inverse of 3 mod 11 using Extended Euclidean

Find x such that 3x ≡ 1 (mod 11), i.e., solve: 3x + 11y = 1

```
Step 1: gcd(11, 3)
11 = 3 × 3 + 2   →  2 = 11 - 3 × 3
 3 = 1 × 2 + 1   →  1 = 3 - 1 × 2
 2 = 2 × 1 + 0

Step 2: Back-substitute
1 = 3 - 1 × 2
  = 3 - 1 × (11 - 3 × 3)
  = 3 - 11 + 3 × 3
  = 4 × 3 - 1 × 11

∴ x = 4,  y = -1
Verification: 3 × 4 = 12 ≡ 1 (mod 11) ✓
```

**∴ Multiplicative inverse of 3 mod 11 = 4**

### Example 2: Find inverse of 7 mod 26 (used in affine cipher)

```
gcd(26, 7):
26 = 3 × 7 + 5
 7 = 1 × 5 + 2
 5 = 2 × 2 + 1
 2 = 2 × 1 + 0

Back-substitute:
1 = 5 - 2 × 2
  = 5 - 2 × (7 - 5)
  = 3 × 5 - 2 × 7
  = 3(26 - 3×7) - 2×7
  = 3×26 - 9×7 - 2×7
  = 3×26 - 11×7

So: -11 × 7 ≡ 1 (mod 26)
    -11 mod 26 = 15

∴ Multiplicative inverse of 7 mod 26 = 15
Verify: 7 × 15 = 105 = 4×26 + 1 ≡ 1 (mod 26) ✓
```

---

## 4. Fermat's Little Theorem

### Statement

If **p is a prime** and **a is not divisible by p**, then:

```
a^(p-1) ≡ 1 (mod p)
```

Equivalently:
```
a^p ≡ a (mod p)
```

### Why It Matters in Cryptography

- Forms the basis of **RSA** encryption
- Used to compute **modular inverses** when modulus is prime:
  ```
  a^(-1) ≡ a^(p-2) (mod p)
  ```

### Proof Sketch

Consider the set {1, 2, 3, ..., p-1}. Multiply each element by a:
{a, 2a, 3a, ..., (p-1)a} — these are all distinct mod p and form the same set.

Therefore:
```
a × 2a × 3a × ... × (p-1)a ≡ 1 × 2 × 3 × ... × (p-1) (mod p)
a^(p-1) × (p-1)! ≡ (p-1)! (mod p)
a^(p-1) ≡ 1 (mod p)  [since gcd((p-1)!, p) = 1]
```

### Example Problems

**Example 1:** Compute 3^201 mod 11

```
p = 11 (prime), a = 3, gcd(3,11) = 1

By Fermat's: 3^10 ≡ 1 (mod 11)

201 = 10 × 20 + 1

3^201 = 3^(10×20) × 3^1
      = (3^10)^20 × 3
      ≡ 1^20 × 3 (mod 11)
      ≡ 3 (mod 11)

∴ 3^201 mod 11 = 3
```

**Example 2:** Compute 7^222 mod 11

```
p = 11, By Fermat's: 7^10 ≡ 1 (mod 11)

222 = 10 × 22 + 2

7^222 = (7^10)^22 × 7^2
      ≡ 1^22 × 49 (mod 11)
      ≡ 49 mod 11
      ≡ 5 (mod 11)

∴ 7^222 mod 11 = 5
```

**Example 3:** Find inverse of 6 mod 13 using Fermat's theorem

```
p = 13 (prime)
6^(-1) ≡ 6^(13-2) ≡ 6^11 (mod 13)

6^1  = 6
6^2  = 36 ≡ 10 (mod 13)
6^4  = 10^2 = 100 ≡ 9 (mod 13)
6^8  = 9^2 = 81 ≡ 3 (mod 13)

6^11 = 6^8 × 6^2 × 6^1
     = 3 × 10 × 6 (mod 13)
     = 180 mod 13
     = 180 - 13×13 = 180 - 169 = 11

∴ 6^(-1) ≡ 11 (mod 13)
Verify: 6 × 11 = 66 = 5×13 + 1 ≡ 1 (mod 13) ✓
```

---

## 5. Euler's Theorem & Totient Function

### Euler's Totient Function φ(n)

φ(n) = number of integers in {1, 2, ..., n} that are **coprime** to n (i.e., gcd(a,n) = 1)

### Formulas

| n | φ(n) formula | Example |
|---|---|---|
| p (prime) | φ(p) = p - 1 | φ(7) = 6 |
| p² | φ(p²) = p² - p | φ(9) = 6 |
| pq (distinct primes) | φ(pq) = (p-1)(q-1) | φ(15) = 8 |
| General | φ(n) = n × ∏(1 - 1/p) for prime p|n | |

### Computing φ(n) — Examples

**φ(12):**
```
12 = 2² × 3
φ(12) = 12 × (1 - 1/2) × (1 - 1/3)
       = 12 × 1/2 × 2/3
       = 4

Verify: {1, 5, 7, 11} are coprime to 12 → 4 numbers ✓
```

**φ(30):**
```
30 = 2 × 3 × 5
φ(30) = 30 × (1-1/2)(1-1/3)(1-1/5)
       = 30 × 1/2 × 2/3 × 4/5 = 8
```

**φ(36):**
```
36 = 2² × 3²
φ(36) = 36 × (1-1/2)(1-1/3) = 36 × 1/2 × 2/3 = 12
```

### Euler's Theorem

If **gcd(a, n) = 1**, then:
```
a^φ(n) ≡ 1 (mod n)
```

> 📝 Note: Fermat's Little Theorem is a special case of Euler's Theorem when n = p (prime), since φ(p) = p-1.

### Example Problems

**Example 1:** Compute 7^100 mod 48

```
gcd(7, 48) = 1 ✓
φ(48) = φ(16 × 3) = φ(16) × φ(3) = 8 × 2 = 16

By Euler's Theorem: 7^16 ≡ 1 (mod 48)

100 = 16 × 6 + 4

7^100 = (7^16)^6 × 7^4
      ≡ 1^6 × 7^4 (mod 48)
      = 2401 mod 48
      = 2401 - 50×48 = 2401 - 2400 = 1

∴ 7^100 mod 48 = 1
```

**Example 2:** Compute 3^100 mod 14

```
φ(14) = φ(2×7) = 1 × 6 = 6
gcd(3, 14) = 1 ✓

3^6 ≡ 1 (mod 14)

100 = 6 × 16 + 4

3^100 ≡ 3^4 = 81 mod 14
      = 81 - 5×14 = 81 - 70 = 11

∴ 3^100 mod 14 = 11
```

**Example 3:** Solve x^86 ≡ 6 (mod 13)

```
p = 13, φ(13) = 12
By Fermat's: x^12 ≡ 1 (mod 13)

x^86 = x^(12×7 + 2) = (x^12)^7 × x^2 ≡ x^2 (mod 13)

So: x^2 ≡ 6 (mod 13)
Try x = 1..12:
x=7: 49 mod 13 = 10 ✗
x=8: 64 mod 13 = 12 ✗ (13×4=52, 64-52=12)
x=9: 81 mod 13 = 3 ✗
Actually: 6 mod 13... try x=5: 25 mod 13 = 12 ✗
Try all: No perfect square root exists → equation has no solution
```

---

## 6. Classic Encryption Techniques

### Caesar Cipher (Shift Cipher)

Each letter is shifted by a fixed number k.

```
Encryption: C = (P + k) mod 26
Decryption: P = (C - k) mod 26
```

**Example:** Encrypt "HELLO" with key k = 3
```
H → (7+3) mod 26 = 10 → K
E → (4+3) mod 26 = 7  → H
L → (11+3) mod 26 = 14 → O
L → 14 → O
O → (14+3) mod 26 = 17 → R

Ciphertext: KHOOR
```

### Affine Cipher

```
Encryption: C = (aP + b) mod 26
Decryption: P = a^(-1)(C - b) mod 26

Condition: gcd(a, 26) = 1
Valid values of a: 1,3,5,7,9,11,15,17,19,21,23,25
```

**Example:** Encrypt "HELLO" with a=7, b=3

```
H=7:  (7×7 + 3) mod 26 = 52 mod 26 = 0  → A
E=4:  (7×4 + 3) mod 26 = 31 mod 26 = 5  → F
L=11: (7×11+ 3) mod 26 = 80 mod 26 = 2  → C
L=11: → C
O=14: (7×14+ 3) mod 26 = 101 mod 26 = 23 → X

Ciphertext: AFCCX
```

### Vigenère Cipher

A polyalphabetic substitution cipher using a keyword.

```
Encryption: C_i = (P_i + K_i) mod 26
Decryption: P_i = (C_i - K_i) mod 26
```

**Example:** Encrypt "ATTACKATDAWN" with key "LEMON"

```
Plaintext:  A T T A C K A T D A W N
Key:        L E M O N L E M O N L E
Key nums:   11 4 12 14 13 11 4 12 14 13 11 4

A+L = 0+11 = 11 → L
T+E = 19+4 = 23 → X
T+M = 19+12= 31 mod 26 = 5 → F
A+O = 0+14 = 14 → O
C+N = 2+13 = 15 → P
K+L = 10+11= 21 → V
...

Ciphertext: LXFOPVEFRNHR
```

---

## 7. Symmetric Cipher Model

### Overview

In a **symmetric cipher**, the same key is used for both encryption and decryption.

```
          Key K                    Key K
            │                       │
            ▼                       ▼
Plaintext ──►[Encryption]──► Ciphertext ──►[Decryption]──► Plaintext
   P          Algorithm          C            Algorithm         P

    C = E(K, P)                P = D(K, C)
```

### Components

```
┌─────────────────────────────────────────────────────┐
│              SYMMETRIC CIPHER MODEL                  │
│                                                      │
│  ┌──────────┐    ┌───────────┐    ┌──────────────┐  │
│  │Plaintext │───►│Encryption │───►│  Ciphertext  │  │
│  │    P     │    │ Algorithm │    │      C       │  │
│  └──────────┘    └─────┬─────┘    └──────┬───────┘  │
│                        │                 │           │
│                   ┌────▼────┐       ┌────▼────┐      │
│                   │  Key K  │       │  Key K  │      │
│                   └─────────┘       └────┬────┘      │
│                                          │           │
│                                    ┌─────▼─────┐    │
│                                    │Decryption │    │
│                                    │ Algorithm │    │
│                                    └─────┬─────┘    │
│                                          │           │
│                                    ┌─────▼─────┐    │
│                                    │Plaintext P│    │
│                                    └───────────┘    │
└─────────────────────────────────────────────────────┘
```

### Requirements for Symmetric Cipher Security

1. **Strong encryption algorithm** — Even knowing the algorithm and several (plaintext, ciphertext) pairs, an attacker cannot determine the key or future plaintext.
2. **Secret key** — Sender and receiver must have copies of the key and must keep it secret.

### Types of Symmetric Ciphers

| Type | Examples | Description |
|------|----------|-------------|
| **Stream Cipher** | RC4, A5/1 | Encrypts one bit/byte at a time |
| **Block Cipher** | DES, AES, 3DES | Encrypts fixed-size blocks |

### Cryptanalysis Attacks on Symmetric Ciphers

| Attack Type | What Attacker Knows |
|-------------|---------------------|
| Ciphertext only | Only ciphertext |
| Known plaintext | Some (plaintext, ciphertext) pairs |
| Chosen plaintext | Can choose plaintext, get ciphertext |
| Chosen ciphertext | Can choose ciphertext, get plaintext |

---

## 8. Playfair Cipher

### Overview

The **Playfair Cipher** is a digraph substitution cipher — it encrypts **pairs of letters** at a time using a 5×5 key matrix.

### Key Matrix Construction

1. Write the keyword (remove duplicates, treat I=J)
2. Fill remaining letters of alphabet in order

**Example Keyword: "MONARCHY"**

```
Remove duplicates: M-O-N-A-R-C-H-Y

Key Matrix:
┌───┬───┬───┬───┬───┐
│ M │ O │ N │ A │ R │
├───┼───┼───┼───┼───┤
│ C │ H │ Y │ B │ D │
├───┼───┼───┼───┼───┤
│ E │ F │ G │ I │ K │
├───┼───┼───┼───┼───┤
│ L │ P │ Q │ S │ T │
├───┼───┼───┼───┼───┤
│ U │ V │ W │ X │ Z │
└───┴───┴───┴───┴───┘
```

### Encryption Rules

**Step 1: Prepare plaintext**
- Split into digraphs (pairs)
- If both letters in a pair are same → insert 'X' between them
- If odd number of letters → append 'X'

**Step 2: For each digraph (P1, P2):**

```
RULE 1: Same Row
  → Replace each with letter to its RIGHT (wrap around)

RULE 2: Same Column
  → Replace each with letter BELOW it (wrap around)

RULE 3: Rectangle (different row and column)
  → P1 → same row as P1, column of P2
  → P2 → same row as P2, column of P1
```

### Encryption Example

**Keyword:** MONARCHY  
**Plaintext:** "BALLOON"

```
Step 1: Prepare digraphs
B-A-L-L-O-O-N
Pair: BA LL OO N
LL → insert X: BA LX LO ON
Odd → no issue (4 pairs)

Digraphs: BA  LX  LO  ON

Matrix (MONARCHY):
M O N A R
C H Y B D
E F G I K
L P Q S T
U V W X Z
```

**BA:** B(row=1,col=3) A(row=0,col=3) → Same Column → go DOWN
```
B → I  (B is at row 1, col 3; below is I at row 2, col 3)
A → B  (A is at row 0, col 3; below is B at row 1, col 3)
BA → IB
```

**LX:** L(row=3,col=0) X(row=4,col=3) → Rectangle
```
L → same row as L, col of X → row 3, col 3 = S
X → same row as X, col of L → row 4, col 0 = U
LX → SU
```

**LO:** L(row=3,col=0) O(row=0,col=1) → Rectangle
```
L → row 3, col 1 → P
O → row 0, col 0 → M
LO → PM
```

**ON:** O(row=0,col=1) N(row=0,col=2) → Same Row → go RIGHT
```
O → N
N → A
ON → NA
```

**Ciphertext: IB SU PM NA**

### Decryption Rules

Reverse of encryption:
- Same row → shift LEFT
- Same column → shift UP
- Rectangle → same rectangle rule (symmetric)

### Strengths & Weaknesses

| Strengths | Weaknesses |
|-----------|------------|
| 26×26 = 676 digraphs (harder than mono) | Only 25 possible keys for frequency analysis |
| Hides single-letter frequency | Digraph frequency analysis still possible |
| Simple to implement | Known plaintext attack is easy |

---

## 9. Hill Cipher

### Overview

The **Hill Cipher** is a polygraphic substitution cipher that uses **matrix multiplication** in modular arithmetic.

- Encrypts m letters at a time using an m×m **key matrix K**
- K must be invertible mod 26 (i.e., det(K) must be coprime to 26)

### Encryption Formula

```
C = K × P (mod 26)

Where:
  P = column vector of m plaintext letters (numerical values)
  K = m×m key matrix
  C = column vector of m ciphertext letters
```

### Decryption Formula

```
P = K^(-1) × C (mod 26)

K^(-1) = inverse of K modulo 26
```

### Inverse of 2×2 Matrix mod 26

For K = [[a,b],[c,d]]:
```
det(K) = ad - bc
K^(-1) = det(K)^(-1) × [[d, -b], [-c, a]]  (mod 26)
```

---

### Example 1: 2×2 Hill Cipher

**Key matrix:**
```
K = | 3  3 |
    | 2  5 |
```

**Plaintext:** "HELP" → H=7, E=4, L=11, P=15

**Encrypt in pairs:**

*Pair 1: HE → [7, 4]^T*
```
C1 = K × [7,4]^T mod 26

= | 3×7 + 3×4 |  = | 21+12 |  = | 33 |  = | 7 |  → H
  | 2×7 + 5×4 |    | 14+20 |    | 34 |    | 8 |  → I
```

*Pair 2: LP → [11, 15]^T*
```
C2 = K × [11,15]^T mod 26

= | 3×11 + 3×15 |  = | 33+45 |  = | 78 |  = | 0  |  → A
  | 2×11 + 5×15 |    | 22+75 |    | 97 |    | 19 |  → T
```

**Ciphertext: HIAT**

---

### Example 2: Full 2×2 Hill Cipher with Decryption

**Key:**
```
K = | 6  24 |
    | 1  13 |
```

**Plaintext:** "ACT" — but let's do 2 letters: AC

A=0, C=2

```
C = | 6×0 + 24×2 |  = | 48 |  = | 22 |  → W
    | 1×0 + 13×2 |    | 26 |    | 0  |  → A
```

**For decryption:**

det(K) = 6×13 - 24×1 = 78 - 24 = 54
54 mod 26 = 2
Inverse of 2 mod 26 = 13  (since 2×13=26≡0... not valid!)

> ⚠️ Key must satisfy gcd(det(K), 26) = 1

**Better example with K = [[3,3],[2,5]]:**
```
det = 3×5 - 3×2 = 15-6 = 9
gcd(9,26) = 1 ✓

K^(-1) mod 26:
= 9^(-1) × | 5  -3 | mod 26
            | -2   3 |

9^(-1) mod 26: 9×3=27≡1 mod 26 → 9^(-1) = 3

K^(-1) = 3 × | 5  -3 | mod 26
              | -2   3 |

= | 15  -9 | mod 26  = | 15  17 |
  | -6   9 |           | 20   9 |
```

### Example 3: 3×3 Hill Cipher

**Key:**
```
K = | 6  24  1 |
    | 13 16  10|
    | 20 17  15|
```

**Plaintext:** "ACT" → A=0, C=2, T=19

```
C = K × [0, 2, 19]^T mod 26

Row 1: 6×0 + 24×2 + 1×19 = 0 + 48 + 19 = 67 mod 26 = 15 → P
Row 2: 13×0 + 16×2 + 10×19 = 0 + 32 + 190 = 222 mod 26 = 14 → O
Row 3: 20×0 + 17×2 + 15×19 = 0 + 34 + 285 = 319 mod 26 = 7 → H

Ciphertext: POH
```

### Summary: Hill Cipher Properties

```
┌──────────────────────────────────────────────────────┐
│                  HILL CIPHER SUMMARY                  │
├──────────────────┬───────────────────────────────────┤
│ Key              │ m×m invertible matrix mod 26       │
│ Block size       │ m letters at a time                │
│ Encryption       │ C = KP mod 26                      │
│ Decryption       │ P = K⁻¹C mod 26                    │
│ Key space        │ All invertible m×m matrices mod 26 │
│ Vulnerability    │ Known-plaintext attack             │
│ Strength         │ Hides letter frequency completely  │
└──────────────────┴───────────────────────────────────┘
```

---

## 10. Previous Year Questions Solved

---

### Q: What is three-address code? Generate three-address code for:
```
while (a<b) do
  if(c<d) then
    x:=y+z
  else
    x:=y-z
```

*This is from SP&CC syllabus — refer to compiler notes for three-address code.*

---

### Q: Compute FIRST and FOLLOW — *(SP&CC topic, not CNS)*

---

### CNS-Style Solved Problems

**Q1. Using Fermat's theorem, find 3^(201) mod 11**

```
p=11 (prime), gcd(3,11)=1
Fermat's: 3^10 ≡ 1 (mod 11)
201 = 10×20 + 1
3^201 ≡ 3^1 = 3 (mod 11)   ✓
```

**Q2. Find gcd(4655, 12075) using Euclidean Algorithm**

```
12075 = 2×4655 + 2765
 4655 = 1×2765 + 1890
 2765 = 1×1890 + 875
 1890 = 2×875  + 140
  875 = 6×140  + 35
  140 = 4×35   + 0

gcd(4655, 12075) = 35
```

**Q3. Compute φ(n) for n = 100, 45, 13**

```
φ(100) = φ(4×25) = φ(4)×φ(25) = 2×20 = 40
φ(45)  = φ(9×5)  = φ(9)×φ(5)  = 6×4  = 24
φ(13)  = 13-1 = 12  (13 is prime)
```

**Q4. Encrypt "COME HOME" using Playfair cipher with key "SECURITY"**

**Key matrix with "SECURITY":**
```
Remove duplicates: S-E-C-U-R-I-T-Y

S E C U R
I T Y A B
D F G H K
L M N O P
Q V W X Z
```

Plaintext: COME HOME
Pairs: CO ME HO ME X (pad with X if needed)

**CO:** C(0,2) O(3,3) → Rectangle → C goes to col 3 → U; O goes to col 2 → N → **UN**

**ME:** M(3,1) E(0,1) → Same Column → M→V, E→T → **VT**  
*(M is at row 3 col 1; below→row 4 col 1=V; E at row 0 col 1→below=T)*

**HO:** H(2,3) O(3,3) → Same Column → H→O, O→X → **OX**

**ME:** → **VT** (same as above)

**Ciphertext: UN VT OX VT**

---

**Q5. Encrypt "HILL" using Hill Cipher with K = [[3,3],[2,5]]**

```
H=7, I=8, L=11, L=11

Pair 1: HI → [7,8]
C1 = |3×7+3×8| = |21+24| = |45| mod 26 = |19| → T
     |2×7+5×8|   |14+40|   |54|           | 2| → C

Pair 2: LL → [11,11]
C2 = |3×11+3×11| = |33+33| = |66| mod 26 = |14| → O
     |2×11+5×11|   |22+55|   |77|           | 25| → Z

Ciphertext: TCOZ
```

---

## 📖 Quick Reference Formulas

```
┌──────────────────────────────────────────────────────────┐
│                   FORMULA CHEAT SHEET                     │
├──────────────────────────┬───────────────────────────────┤
│ GCD Euclidean            │ gcd(a,b) = gcd(b, a mod b)    │
│ Extended GCD             │ ax + by = gcd(a,b)            │
│ Fermat's Theorem         │ a^(p-1) ≡ 1 (mod p)           │
│ Euler's Theorem          │ a^φ(n) ≡ 1 (mod n)            │
│ Euler Totient (prime)    │ φ(p) = p - 1                  │
│ Euler Totient (pq)       │ φ(pq) = (p-1)(q-1)            │
│ Mod Exponentiation       │ Square-and-multiply method     │
│ Mod Inverse (prime mod)  │ a^(-1) ≡ a^(p-2) (mod p)     │
│ Caesar Cipher            │ C = (P + k) mod 26            │
│ Affine Cipher            │ C = (aP + b) mod 26           │
│ Hill Cipher Enc          │ C = KP mod 26                 │
│ Hill Cipher Dec          │ P = K^(-1)C mod 26            │
│ Vigenere Enc             │ C_i = (P_i + K_i) mod 26      │
└──────────────────────────┴───────────────────────────────┘
```

---

## 🧠 Common Mistakes to Avoid

1. **Fermat's Theorem** — only valid when p is prime AND gcd(a,p) = 1
2. **Hill Cipher key** — always check gcd(det(K), 26) = 1 before using
3. **Playfair** — I and J are treated as same; always insert X between double letters
4. **Extended GCD** — track signs carefully during back-substitution
5. **Modular inverse** — only exists when gcd(a,n) = 1
6. **Euler's Totient** — φ(1) = 1, φ(2) = 1, φ(prime) = prime - 1

---

*Notes compiled for BE Computer Engineering — Semester VI | Cryptography & Network Security*

