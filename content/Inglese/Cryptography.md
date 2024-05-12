### Cryptography

> [!important] Cryptography 
> The practice (& study) of hiding info so that only those who are intended to access it can and can read and process it. 

Nowadays, cryptography is associated with the scrambling of plaintext (or cleartext, just ordinary text) into ciphertext through encryption (and deciphered through decryption).

##### Encryption

> [!important] Encryption
> Process of transforming info using an algorithm (or cipher) to make it unreadable to anyone except for those possessing a key.
> The result of this process is the encrypted data

##### Decryption

> [!important] Decryption
> The opposite process of encryption, it takes place when the key is used to convert the encrypted data back to plaintext.

##### Keys

Keys are usually strings of 64 binary digits (56 random and 8 for error detection).

##### Types of cryptography

###### Private key cryptography

(Or *symmetrical cryptography*) is based on the fact that both hosts encrypt and decrypt with the same private key. The problem with this one is the fact that the hosts need to exchange the key in a safe and reserved way, so that it isn't intercepted by malicious users.

###### Public key cryptography

(Or *asymmetrical cryptography*) uses 2 keys:

- The receiver's public key, which is distributed and used by the sender to encrypt the message (although it's not possible to decrypt the message it),
- The receiver's private key, which is used by it to decrypt the message encrypted with the public key.

#### Digital signatures

These are an example of public key cryptography, since: a message is signed with the sender's private key so that it can be verified by anyone who has access to the associated public key.

### Objectives

###### Confidentiality

The info must not be understood by people whom it wasn't intended.

###### Integrity

The info must not be altered between the sender and the receiver (not in storage nor transit) without the alteration being detected.

###### Non-repudiation

A sender cannot deny its intentions in creating or transmitting info.

###### Authentication

The sender and receiver must confirm each other's identity and the origin/destination of the info.

