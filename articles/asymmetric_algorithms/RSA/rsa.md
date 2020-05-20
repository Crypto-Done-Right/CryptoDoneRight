---
layout: page
title: RSA
type: asymmetric_algorithms
update: Last Updated Thu, 12 Dec 2018 12:00:01 -0400
permalink: /articles/asymmetric_algorithms/rsa/rsa.html
alerts:
  - id: 1
    type: success
    description: "With proper configuration, RSA signatures are safe to use."
    link: ""
  - id: 2
    type: danger
    description: "RSA encryption (typically used for key exchange) is NOT secure and
    should not be used."
    link: ""
  - id: 3
    type: warning
    description: "While RSA signatures CAN be used safely, there are a number of
    configurations that are not secure. Consider using a more modern algorithm,
    such as ECDSA. If RSA must be used, follow the guidelines and best practices
    outlined in this guide."
    link: ""
further-reading:

related-articles:

warnings:
  - name: Do not use RSA For Encryption
    description: "RSA encryption is generally being deprecated. For key exchange, key agreement, using a protocol such as Diffie Hellman (DH), is almost always better."

best_practices:
  - name: Use 2048-bit, or Larger, Keys.
    description: "When possible, use 256-bit keys. This is especially true for data that may remain encrypted for very long periods of time."
  - name: Use PSS Padding for Signatures.
    description: "Although there are no known attacks against PKCSv1.5 for signatures, it is recommended to use the PSS padding scheme."

---
RSA is an asymmetric algorithm (a refresher on asymmetric cryptography can be found [here](/articles/concepts/asymmetric_cryptography.html)) named for Rivest, Shamir, and Adleman, the three cryptographers that publicly presented about the system in 1977. RSA was one of the first asymmetric algorithms described and is still one of the most widely used. Nevertheless, more modern algorithms are often recommended for both performance and security reasons.

Unlike many asymmetric algorithms, RSA can actually be used to encrypt small messages. In particular, what is encrypted with the public key can be decrypted with the private key, and what is encrypted with the private key can be decrypted with the public key.

For creating digital signatures, a party with control of an RSA private key can take arbitrary data, compute a hash value (of fixed size), and then encrypt the hash with the private key. The encrypted hash is the RSA digital signature. Assuming that a verifying party is in possession of the correct and corresponding public key, the verifier can assure themselves that the data was "signed" by the first party by using the public key to decrypt the signature to obtain the unencrypted hash, compute a new hash over the data, and then ensure that the new hash and the decrypted hash are identical.

While the concept is relatively simple, there are many devils in the details. First and foremost, the second party must have some assurance that they possess the correct public key. There are many ways for an attacker to trick a verifier into accepting a false public key. One of the most common ways of securing the public key is to use certificates and a public-key infrastructure.

Another potential problem with digital signatures is that the RSA encryption mechanism is not considered secure without a proper padding algorithm. At present, the recommended padding algorithms for digital signatures is PSS.

In addition to signature functions, RSA can be used for key exchange. In TLS 1.2 and earlier, one side could encrypt a session key (or a session pre-key) using the public key of the other participant. Once received, the RSA private key decrypted the session pre-key. This process of sending an asymmetrically encrypted session (pre-)key is a key-transport mechanism for key-exchange.

An example flow of how this might work is as follows... <br>
> 1. Alice has a key pair; she guards the private key and publishes the public key.
> 2. Bob wants to communicate securely with Alice, so he uses her published public key to encrypt a request to communicate and sends it to her. In his message he may include a secret key to be used with AES.
> 3. Alice receives an encrypted message and uses her private key to decrypt. She sees the AES secret key, encrypts a message using AES and sends it to Bob.
> 4. Now Bob and Alice are able to communicate relatively efficiently using AES.

The problem with encryption is that the padding scheme is even more critical and a number of attacks were found against PKCSv1.5, an early padding scheme used in TLS 1.2. Even though newer padding schemes are supposed to be more secure, the consensus in the cryptographic community is simply to stop using RSA encryption altogether. If RSA encryption must be used, it must be used with OAEP padding.

For more details on key generation, encryption, decryption, signatures, deployment, and usage, please look in the quick start guides listed below.
