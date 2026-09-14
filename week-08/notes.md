# Week 8 Notes — Practical Cryptography

**Student Name:** Catasia Williams

**Date:** September 13, 2026

## Vocabulary in My Own Words

- Plaintext: Information in its original readable form/readable data before anything protects it. 
- Ciphertext: The unreadable output of encryption
- Encryption: Transforming readable data into unreadable data using a key, so that only someone with the right key can read it.
- Hash / digest The fixed-length output of a hash function — the fingerprint itself. Comparing two digests tells you whether two files are identical without reading either one.
- Public key: The half of a key pair you are meant to hand out freely. Others use it to encrypt to you, or to verify something you signed. Public does not mean weak.
- Private key: The half of a key pair that never leaves your possession. It decrypts what was encrypted to you and signs on your behalf — so whoever holds it can act as you.
- Digital signature: A value produced from a file's digest and th/ A cryptographic signature created with a private key that helps verify the integrity and authenticity of signed data. signer's private key. Anyone with the matching public key can verify it, which proves the file has not changed and that the holder of that private key signed it.
- `authorized_keys`: A file in the account's ~/.ssh directory on the server listing the public keys allowed to log in as that account. Adding the public key here is what grants access.

## Command-to-Purpose Map

| Command | What it demonstrated |
| --- | --- |
| `openssl enc` | Encryption and decryption of data (confidentiality). |
| `sha256sum` | Hashing which is used to compare file digests and detect changes. |
| `ssh-keygen` | Creation of an SSH public and private key pair and its fingerprint.  |
| `openssl dgst` | Create an verify digital signatures (integrity and authentication). |
| `ssh ... -o PasswordAuthentication=no` | Forced public-key authentication (successful SSH login using the key, not account password) |

## Safety Rules I Must Remember

1. Your private key never leaves your machine
2. Only put public keys in authorized_keys; never put private keys there.
3. If a private key is ever exposed, treat it as compromised: generate a new pair and replace the public key.

## Question for the Instructor
