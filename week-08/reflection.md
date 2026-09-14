# Week 8 Reflection — Practical Cryptography

**Student Name:** Catasia Williams

**Date:** September 13, 2026

Answer each question in 3–5 sentences.

1. How are encryption and hashing different?

```text
Encryption translates plaintext into ciphertext for confidentiality. The information can be decrypted to be turned back to plaintext. Hashing transform data into a fixed-length hash or digest for the purpose of comparing the data to ensure integrity. Hashing is not designed to convert the digest back to its original state. 
```

2. How are symmetric and asymmetric cryptography different?

```text
Symmetric cryptography: Encryption where the same single key both locks and unlocks the data — like one combination that both closes and opens a hotel room safe.
Asymmetric cryptography: Cryptography using two mathematically linked keys instead of one, where each key does a job the other cannot. Also called public-key cryptography.

Symmetric cryptography uses the same key to encrypt and decrypt data. Asymmetric cryptography uses a pair of keys (public and private keys) for encryption, decryption, and digital signatures. AES is the symmetric encryption standard used.
```

3. Why does a private key need stronger protection than a public key?

```text
A private key needs stronger protection than a public key because the private key decrypts information and creates digital signatures. It helps unlock protected information and prove possession of the private key. The public key is designed to be shared, so it does not require the same level of confidentiality. 
```

4. What changed between Week 6 password-based SSH and Week 8 key-based SSH? What stayed the same?

```text
The main thing that changed was the authentication method. Week 6 authentication was based on a password (the analyst account password). Week 8 SSH logins were based on using the SSH private key and its passphrase with the matching public key. The things that stayed the same are the purpose of authentication, the VM, the account, and using SSH. 
```

5. Which Week 8 task felt most connected to a real cybersecurity job, and why?

```text
The key authentication felt most connected to a real cybersecurity job because I had to protect the private key with a passphrase. Protecting private keys is important to prevent unauthorized access to information, which can lead to malicious activity. 
```

6. What question do you have about certificates, identity, or trust before Week 9?

```text
I'm interested in learning about certificates because this concept is new to me. I am interested in learning how certificates connect to the concepts I learned this week. 
```
