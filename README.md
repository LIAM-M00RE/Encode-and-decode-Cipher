# Encode-and-decode-Cipher

A small Java command-line program that encrypts and decrypts text with a **Caesar cipher**.

## Files

| File | Purpose |
| --- | --- |
| `encode.java` | Takes a word and a shift key, prints the encrypted text |
| `decode.java` | Takes a word and a shift key, prints the decrypted text |

## How it works

Each letter is shifted a fixed number of places along the alphabet, wrapping from `z` back to `a`.

```
Encrypt:  C = (P + k) mod 26
Decrypt:  P = (C - k) mod 26
```

With a key of `3`, `hello` becomes `khoor`.

Both programs lowercase the input, look up each character's position in the string `"abcdefghijklmnopqrstuvwxyz"`, apply the shift with modulo 26, and build the output one character at a time. Decryption also corrects negative results so the index wraps round correctly.

## Usage

Requires Java 11 or newer.

```bash
java encode.java
java decode.java
```

Example:

```
Enter the String for Encryption:hello

Enter Shift Key:
3

Encrpyted msg:khoor
```

The program reads a single word (up to the first space) and an integer key.

## Evaluating the Caesar cipher

The Caesar cipher is a monoalphabetic substitution cipher: every plaintext letter always maps to the same ciphertext letter. That makes it a good teaching tool and a poor security tool.

**Strengths**
- Very simple to implement and understand
- Needs no special libraries, just modular arithmetic
- Useful for illustrating core ideas: keys, encryption vs decryption, and why secrecy shouldn't depend on hiding the algorithm

**Weaknesses**
- **Tiny keyspace.** Only 25 useful keys (a shift of 0 or 26 changes nothing), so an attacker can try every one in seconds, by hand or by script.
- **Letter frequencies survive.** Because each letter always maps to the same one, the most common ciphertext letter is likely to stand for `e` in English. Frequency analysis recovers the key from even short messages.
- **No diffusion or confusion.** Changing one plaintext letter changes only one ciphertext letter, and the key's relationship to the output is trivial.
- **Trivial known-plaintext attack.** One known plaintext/ciphertext letter pair reveals the key immediately.
- **Preserves structure.** Word lengths, repeated letters, and patterns remain visible (when spaces are kept).
- **Obeys Kerckhoffs's principle badly.** Security rests on a 1-in-25 guess, which is not meaningful.

**Verdict:** fine for learning and puzzles, but it offers no real confidentiality. Modern ciphers such as AES use keyspaces of 2^128 or larger, multiple rounds of substitution and permutation, and are designed so that statistical patterns in the plaintext do not show up in the ciphertext.

## Notes on current behaviour

- Designed for lowercase letters a–z; other characters (digits, punctuation, spaces) are not handled
- Single-word input only
- Intended for education, not for protecting real data
