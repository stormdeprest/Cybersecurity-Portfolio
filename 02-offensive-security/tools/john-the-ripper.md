# Password Cracking with Hashcat & John the Ripper

## Hashcat

## Basic Syntax

`hashcat -m <hash_type> -a <attack_mode> hashfile wordlist`

**Parameters:**

- `-m <hash_type>` - Specifies the hash type in numeric format (e.g., `-m 1000` for NTLM)
    
    - Check the [official documentation](https://hashcat.net/wiki/doku.php?id=example_hashes) or `man hashcat` to find hash type codes
        
- `-a <attack_mode>` - Specifies the attack mode (e.g., `-a 0` for straight/dictionary attack)
    
- `hashfile` - File containing the hash you want to crack
    
- `wordlist` - The wordlist you want to use in your attack
    

## Example

`hashcat -m 3200 -a 0 hash.txt /usr/share/wordlists/rockyou.txt`

This treats the hash as Bcrypt and tries passwords from the rockyou.txt file.

## John the Ripper

## Basic Syntax

`john --format=[format] --wordlist=[wordlist_path] [hash_file]`

**Example:**

`john --format=raw-md5 --wordlist=/usr/share/wordlists/rockyou.txt hash.txt`

## Unshadow - Linux Password Hashes

## Why Use Unshadow?

On Linux, password hashes are stored in `/etc/shadow`. John the Ripper cannot use these hashes directly because it also needs information from `/etc/passwd` (like usernames).

The two files must first be combined.

## Usage

`unshadow [path_to_passwd] [path_to_shadow] > unshadowed.txt`

**Example:**

`unshadow local_passwd local_shadow > unshadowed.txt`

You can use either complete files or only relevant lines (e.g., only the root user line).

## Cracking with John

After unshadowing, pass the file to John:

`john --wordlist=/usr/share/wordlists/rockyou.txt unshadowed.txt`

## Single Crack Mode

John can guess passwords based on the username in addition to using wordlists. This is called **Single Crack Mode**.

## Word Mangling

John takes a username (e.g., "Markus") and tries variations like:

- Markus1, Markus2, Markus3
    
- MArkus, MARkus, MARKus
    
- Markus!, Markus$, Markus*
    

This is called **word mangling**: John applies rules to create mutations of the username → useful because many people use predictable passwords.

## GECOS Field

In `/etc/passwd`, the 5th field is the GECOS field, which contains information like:

- Full name
    
- Phone number
    
- Office location
    

John uses this extra information for word mangling (e.g., full name → variations of it).

## Usage

`john --single --format=[format] hashfile`

**Example:**

`john --single --format=raw-sha256 hashes.txt`

## Important: Hash File Format

In Single Mode, John needs to know which user the hash belongs to.

The file must be formatted as:

`username:hash`

## Cracking ZIP Files

John the Ripper can crack password-protected ZIP files. You must first convert the ZIP file to a hash format that John can read.

## Zip2John

`zip2john [zipfile] > output.txt`

**Example:**

`zip2john zipfile.zip > zip_hash.txt`

The result is a file with the hash that John can crack.

## Crack with John

`john --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt`

John will attempt to crack the ZIP password using the wordlist.

## RAR Files

Same process with `rar2john`:

`rar2john archive.rar > rar_hash.txt john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt`

## Cracking SSH Key Passphrases

SSH can work with private keys (`id_rsa`) instead of passwords. Sometimes these private keys are protected with a passphrase.

You can crack that passphrase with John the Ripper.

## ssh2john

Convert the `id_rsa` file to a hash that John can read:

`ssh2john id_rsa > id_rsa_hash.txt`

## Crack with John

`john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt`

John will attempt to crack the SSH key's passphrase.

## Other Useful Converters

John includes several `*2john` tools for different file types:

- `gpg2john` - GPG/PGP private keys
    
- `keepass2john` - KeePass database files
    
- `pdf2john` - Password-protected PDFs
    
- `office2john` - Microsoft Office documents