# -IT23039-CT-1-Practicing-Number-Theory
# Number Theory and Cryptography Workshop

**Name:** Afrin  
**Student ID:** IT23039  
**Department:** Information and Communication Technology (ICT)  
**University:** Mawlana Bhashani Science and Technology University (MBSTU)

---

## 1. Introduction

This repository contains my learning materials, Python implementations, assignments, and practical exercises from the **Number Theory and Cryptography Workshop** organized by Maths and Physics Club, IIT Bombay.

The main objective of this workshop is to understand fundamental concepts of Number Theory and Cryptography through mathematical problems, algorithms, and Python programming.

### Topics Covered

- Basic Number Theory
- Greatest Common Divisor (GCD)
- Extended Euclidean Algorithm
- Least Common Multiple (LCM)
- Diophantine Equations
- Modular Arithmetic
- Modular Inverse
- Fast Modular Exponentiation
- Chinese Remainder Theorem
- Prime Numbers and Primality Testing
- RSA Cryptography
- Diffie-Hellman Key Exchange
- Fermat Pseudoprimes
- Many-Time Pad
- Shor's Algorithm

---

## 2. Tools and Technologies

| Tool | Purpose |
|---|---|
| Python 3 | Implementing algorithms |
| Google Colab | Writing and executing Python code |
| Jupyter Notebook | Practical exercises |
| Git and GitHub | Version control and project submission |
| Markdown | Documentation |

---

# 3. Day 1: Number Theory

## 3.1 Greatest Common Divisor (GCD)

The Greatest Common Divisor (GCD) of two integers is the largest positive integer that divides both numbers without leaving a remainder.

**Example:**

\[
GCD(12,8)=4
\]

### Python Implementation

```python
def gcd(a, b):
    while b != 0:
        a, b = b, a % b
    return a

print(gcd(12, 8))
print(gcd(27, 15))
```

**Output:**

```text
4
3
```

## 3.2 Extended Euclidean Algorithm

The Extended Euclidean Algorithm calculates GCD and also finds two integers \(x\) and \(y\) such that:

\[
ax+by=GCD(a,b)
\]

### Python Implementation

```python
def extended_gcd(a, b):
    assert a >= b and b >= 0 and a + b > 0

    if b == 0:
        d, x, y = a, 1, 0
    else:
        d, x1, y1 = extended_gcd(b, a % b)

        x = y1
        y = x1 - (a // b) * y1

    assert a % d == 0 and b % d == 0
    assert d == a * x + b * y

    return (d, x, y)

print(extended_gcd(8, 4))
print(extended_gcd(27, 15))
```

**Output:**

```text
(4, 0, 1)
(3, -1, 2)
```

## 3.3 Least Common Multiple (LCM)

LCM is the smallest positive integer that is divisible by both given integers.

**Formula:**

\[
LCM(a,b)=\frac{a\times b}{GCD(a,b)}
\]

### Python Implementation

```python
def lcm(a, b):
    d, x, y = extended_gcd(max(a, b), min(a, b))
    return (a // d) * b

print(lcm(9, 3))
print(lcm(17, 37))
```

**Output:**

```text
9
629
```

## 3.4 Diophantine Equation

A linear Diophantine equation has the form:

\[
ax+by=c
\]

A solution exists if and only if:

\[
GCD(a,b)\mid c
\]

### Python Implementation

```python
def diophantine(a, b, c):

    if a >= b:
        gcd, x1, y1 = extended_gcd(a, b)
        x, y = x1, y1
    else:
        gcd, x1, y1 = extended_gcd(b, a)
        x, y = y1, x1

    x *= c // gcd
    y *= c // gcd

    assert c % gcd == 0
    assert a * x + b * y == c

    return (x, y)

print(diophantine(34, 51, 170))
print(diophantine(91, 117, 65))
```

**Output:**

```text
(-10, 10)
(20, -15)
```

## 3.5 Modular Inverse

The modular inverse of \(a\) modulo \(n\) is an integer \(x\) satisfying:

\[
ax\equiv1\pmod n
\]

A modular inverse exists if:

\[
GCD(a,n)=1
\]

### Python Implementation

```python
def modInverse(a, n):

    d, x, y = extended_gcd(max(a, n), min(a, n))

    if a >= n:
        inverse = x
    else:
        inverse = y

    return inverse % n
```

## 3.6 Modular Division

Modular division uses the modular inverse.

\[
\frac{b}{a}\pmod n
=
b\times a^{-1}\pmod n
\]

### Python Implementation

```python
def divide(b, a, n):

    assert n > 1 and a > 0

    aInv = modInverse(a, n)

    assert (a * aInv) % n == 1

    return (aInv * b) % n

print(divide(9, 5, 3))
print(divide(223, 67, 54))
```

**Output:**

```text
0
13
```

## 3.7 Fast Modular Exponentiation

Fast Modular Exponentiation calculates:

\[
b^e\bmod m
\]

It uses repeated squaring to reduce the number of modular multiplications.

### Python Implementation

```python
def FastModularExponentiation(b, e, m):

    result = 1
    b = b % m

    while e > 0:

        if e % 2 == 1:
            result = (result * b) % m

        b = (b * b) % m
        e = e // 2

    return result

print(FastModularExponentiation(4, 5, 3))
```

**Output:**

```text
1
```

## 3.8 Chinese Remainder Theorem (CRT)

The Chinese Remainder Theorem finds a number satisfying multiple congruences when the moduli are pairwise coprime.

Given:

\[
x\equiv r_1\pmod{n_1}
\]

\[
x\equiv r_2\pmod{n_2}
\]

### Python Implementation

```python
def ChineseRemainderTheorem(n1, r1, n2, r2):

    d, x, y = extended_gcd(n1, n2)

    assert d == 1

    result = r1 * n2 * y + r2 * n1 * x

    return result % (n1 * n2)

print(ChineseRemainderTheorem(13, 7, 6, 5))
print(ChineseRema
