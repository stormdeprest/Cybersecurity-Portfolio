# Cryptography Basics

## Core Concepts

- **Plaintext:** Readable, original data before encryption
    
- **Ciphertext:** Unreadable, encrypted version of the data
    
- **Cipher:** The algorithm that encrypts and decrypts plaintext
    
- **Key:** Secret sequence of bits used by the cipher for encryption and decryption
    
- **Encryption:** Process that converts plaintext into ciphertext using a cipher and key
    
- **Decryption:** Process that converts ciphertext back into plaintext using the correct key
    

## Symmetric Encryption (Private Key Cryptography)

Uses the **same key** (1 private key) for both encryption and decryption.

**Common algorithms:**

- **DES** - 56-bit key, cracked in 24 hours (obsolete)
    
- **3DES** - 168-bit key
    
- **AES** - Current standard, adopted in 2001. Key sizes: 128, 192, or 256-bit
    

## Asymmetric Encryption (Public Key Cryptography)

Uses **public key** for encryption and **private key** for decryption.

## Mathematical Operations for Encryption

## XOR Operation (Exclusive OR)

Two bits the same = 0, two bits different = 1

|A|B|A ⊕ B|
|---|---|---|
|0|0|0|
|0|1|1|
|1|0|1|
|1|1|0|

**Example:** 1001⊕1010=00111001⊕1010=0011

## Modulo Operation

X % Y returns the remainder after division.

**Examples:**

- 60  12=060mod12=0 → 60 / 12 = 5, nothing remains
    
- 23  6=523mod6=5 → 23 / 6 = 3, remainder 5
    
- 23  7=223mod7=2 → 23 / 7 = 3, remainder 2
    

## RSA (Simplified)

## What is RSA?

RSA is a form of asymmetric encryption used to securely send data over an insecure network (like the internet).

**RSA uses two keys:**

- **Public key** (public) → anyone can use it to send you encrypted data
    
- **Private key** (secret) → only you have it, used to decrypt
    

You can securely send something with RSA without first sharing a secret key.

## How RSA Works (Simple Steps)

1. The receiver creates two keys:
    
    - A public key (for encryption)
        
    - A private key (for decryption)
        
2. The receiver sends their public key to everyone
    
3. Someone wants to send you a message → they encrypt it with your public key
    
4. Only you can decrypt the message, because only you have the private key
    

The complex mathematics ensures it's impossible to guess the private key.

## Example

1. Bob sends his public key to Alice
    
2. Alice encrypts the message with Bob's public key
    
3. Bob uses his private key to read the message
    
4. Nobody else can do this
    

## Why is RSA Secure?

Because it's easy to multiply two large numbers,  
but extremely difficult to factor the result back into those two numbers.  
This makes the private key impossible to guess.

## Diffie-Hellman Key Exchange

## What Does Diffie-Hellman Do?

Diffie-Hellman is a method where two people can create a shared secret key together,  
even if everyone can watch the connection.

**Key points:**

- They never send the secret key over the internet
    
- They both end up with the same secret key
    
- An eavesdropper cannot derive the key
    

## Simple Explanation (Without Math)

1. Alice and Bob openly agree on some shared, non-secret information
    
2. Each chooses their own secret number (their private secret)
    
3. They send each other a calculated public value
    
4. With that value + their own secret, they calculate the same secret key
    
5. A hacker can only see the public info but cannot calculate the secret key
    

## Use Case

Diffie-Hellman is used to create a shared key,  
which is then used for fast symmetric encryption.  
Often used together with RSA (for identity and authentication).

## SSH Authentication

## Server Authentication

**First connection:** SSH shows server public key fingerprint

`Are you sure you want to continue connecting?`

After confirming "yes", the key is saved in:

`~/.ssh/known_hosts`

## Client Authentication (With Keys)

**Generate SSH keys:**

`ssh-keygen -t ed25519`

**Copy public key to server:**

`ssh-copy-id user@host`

**Connect with specific private key:**

`ssh -i id_ed25519 user@host`

## Important About Private Keys

- Never share your private key
    
- Permissions must be correct:
    
    
    `chmod 600 id_ed25519`
    
- Server trusts keys via: `~/.ssh/authorized_keys`
    

## Digital Signatures & Certificates

## Digital Signatures

- In the digital world, a digital signature replaces your physical signature
    
- Proves who created a file and that it hasn't been modified
    
- You sign with your **private key**, others verify with your **public key**
    
- You don't sign the entire document, but a **hash** of the document
    

## Certificates

Certificates prove that a server or person is authentic.

**For websites (HTTPS), this works via a chain of trust:**

`Root CA → trusted → issues certificate → browser trusts website`

- Every browser/OS trusts certain Root Certificate Authorities by default
    
- For your own website, you can get a TLS certificate (e.g., free via Let's Encrypt)
    

## PGP/GPG

## Overview

PGP/GPG is software for encryption and digital signatures, often used for secure email.

## Key Pair

- **Public key** → share with others (so they can encrypt messages to you)
    
- **Private key** → keep private (to decrypt messages or sign something)
    

## Generate Keys

`gpg --full-gen-key`

**Choose:**

- Key type (e.g., ECC or RSA)
    
- Validity period
    
- Your name & email for the key-ID
    

## Key Protection

GPG private keys can be protected with a passphrase (similar to SSH keys).

In CTFs, you can crack passphrases using `gpg2john` + John the Ripper.

## Practical Example

**Share your public key with others** → they encrypt to you

**Decrypt:**

`gpg --decrypt file.gpg`

**New computer? Import your key:**

`gpg --import backup.key`