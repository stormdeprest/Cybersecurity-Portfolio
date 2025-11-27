# Hashing Basics

## What is a Hash Function?

A hash function converts data of any size into a fixed-length output (the hash).

**Key characteristics:**

- It's not encryption → you cannot reverse-calculate from hash to original data
    
- A tiny change in input (1 bit) → completely different hash (avalanche effect)
    
- Hashes are often displayed in hexadecimal (like with `md5sum`, `sha256sum`)
    

## Why is Hashing Important?

- **Integrity checking:** Verify if something has been changed
    
- **Password storage:** Passwords are never stored in plaintext, only their hash
    
- **Authentication:** When logging in, the server hashes your input and compares it with the stored hash
    

## Example Commands

`md5sum file.txt sha1sum file.txt sha256sum file.txt`

## Why Hash Passwords?

You don't store the password, but its hash → safer during data breaches.

**Problem:** Same password = same hash → easy to recognize and vulnerable to rainbow tables.

## What is a Rainbow Table?

A large precomputed list of (hash → password) mappings.

Attackers can quickly find a password based on its hash.

## Solution: Salt

**Salt** = random value, different per user

`Salt + password → hash`

Result: Each hash becomes unique, even for identical passwords.

Modern secure functions like **bcrypt**, **scrypt**, and **Argon2** handle this automatically.

## How to Store Passwords Securely

1. Choose a secure hashing function (Argon2/bcrypt/scrypt)
    
2. Generate unique salt per user
    
3. Hash the combination:
    
    
    `hash = hashfunction(password + salt)`
    
4. Store hash + salt (salt doesn't need to be secret)
    

## Why Not Use Encryption?

Encryption requires a key.

That key must be stored somewhere → if the key is stolen, all passwords are readable.

Hashing is one-way and doesn't require storing a secret key.

## Linux Hashes: How to Recognize Them

In Linux, password hashes are stored in: `/etc/shadow`

Each line has a field with the format:

`$prefix$options$salt$hash`

**Prefix** = hash algorithm

This makes Linux hashes easy to identify.

## Common Linux Hash Prefixes

|Prefix|Hash Type|
|---|---|
|`$y$`|yescrypt (new, strong, modern Linux)|
|`$gy$`|gost-yescrypt|
|`$7$`|scrypt|
|`$2b$` / `$2y$` / `$2a$`|bcrypt|
|`$6$`|sha512crypt|
|`$md5`|SunMD5|
|`$1$`|md5crypt|

## Example: Modern Linux Hash

From `/etc/shadow`:

`strategos:$y$j9T$76UzfgEM5PnymhQ7TlJey1$/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4`

**Split by `$`:**

- `y` → yescrypt (algorithm)
    
- `j9T` → options / parameters
    
- `76UzfgEM5PnymhQ7TlJey1` → salt
    
- `/OOSg64dhfF.TigVPdzqiFang6uZA4QA1pzzegKdVm4` → hash