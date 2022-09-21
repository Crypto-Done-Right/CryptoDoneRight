---
layout: quickstart
title: "Developer's QuickStart"
type: AES-GCM
qtype: dev
upper-link: /articles/symmetric_algorithms/mode_gcm/mode_gcm.html
image: /img/common/NewDevLogo.png
note: "Are you a developer? Get started with crucial implementation details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
alerts:

further-reading:

related-articles:

attacks:
---
## <img src="/img/common/configuration.jpg " style="width:110px;height:100px;" /> AES GCM Mode

**Why GCM Mode**\\
Considered a safe and efficient method of operation. It is a very popular choice for authenticated encryption [MAC](https://crypto.stackexchange.com/questions/12178/why-should-i-use-authenticated-encryption-instead-of-just-encryption).
There are no other advantages from a security standpoint (as long as all modes of operation are configured as per the best practice).

Additonal Reading:  [Matthew Green: How to choose authenticated encryption?](https://blog.cryptographyengineering.com/2012/05/19/how-to-choose-authenticated-encryption/)

**How it works**
* [Galois/Counter Mode](https://en.wikipedia.org/wiki/Galois/Counter_Mode)
* [Difference between AES CBC and GCM](https://crypto.stackexchange.com/questions/12178/why-should-i-use-authenticated-encryption-instead-of-just-encryption). 

**Where is it commonly used**\\
GCM is used in many of the SSL/TLS cipher suites. It has various other applications as listed on this [wiki page](https://en.wikipedia.org/wiki/AES_implementations#Python).

**How to use GCM**
* aes-128-gcm← this is good!
* aes-256-gcm  (with iv = 96bit,tag=128bit) ← this is good too!

**How secure**

<span class="red">GCM requires no padding. This is because CTR mode is also a part of GCM. </span>

As a reminder, CTR mode is special in a few ways:
* Padding doesn't apply and therefore eliminates all the padding attacks that were possible with modes like CCB where padding is required. . Normally, a block encryption algorithm (AES, Blowfish, DES, RC2, etc.) emit encrypted output that is a multiple of the block size (16 bytes for AES as an example). With CTR mode, the number of bytes output is exactly equal to the number of bytes input, so no padding/unpadding is required. The PaddingScheme property does not apply for counter mode.
* CTR mode increments a counter for each subsequent block encrypted. For example, if an application encrypted the string "1234567890" twenty times in a row, using the same instance of the Chilkat Crypt2 object, then each iteration's result would be different. This is because the counter is being incremented. The decrypting application would need to decrypt in exactly the same manner. The 1st decrypt should begin with a new instance of a Crypt2 object so that it's counter is at the initial value of 0. Additionally, GCM mode provides authentication of the message without any additonal calculations.

It would be a mistake to encrypt 20 strings using an instance of the Crypt2 object, and then attempt to decrypt with the same Crypt2 object. To decrypt successfully, the app would need to instantiate a new Crypt2 object and then decrypt, so that the counters match.

<span class="green">Good points:</span>  Secure when done right, parallel encryption and decryption with authentication built in.\\
<span class="red">Bad points:</span>  Not many. It is complicated to implement and can be catostrophical if not implemented correctly.

## <img src="/img/common/implementation.png " style="width:100px;height:100px;" /> AES Implementation

### **Concept**
DO NOT roll your own Crypto! Use standard services and libraries.

It is NOT advisable in any circumstances to develop any sort of cryptography on your own. Instead , there are a few options for standard libraries that can be used. These libraries offer better stability as they are usually a product of several years of experience in implementing cryptography by an active development community who are dedicated towards efforts in implementation. It is therefore considered to be reliable and robust.


#### Examples
OpenSSL is one such library which popular and therefore is used as an example for this concept. OpenSSL is not the only available crypto library. For a list of different libraries and a comparision between them, visit [here](https://en.wikipedia.org/wiki/Comparison_of_cryptography_libraries).

The recommended version of OpenSSL is the latest 1.1.1. Some of them are additon the latest encryption standards and removal of older vulnerable ones.
<br /><br />

## Usage of Cryptography in Programming Languages

### **Concept**
It is again advised to not roll out your own cryptography while developing software. There are popular libraries in almost all programming languages that can readily be used to perform cryptographic operations.
<br /><br />

### Examples
#### Python
There are multiple libraries that support AES in GCM mode. Some of them are:
* PyCrypto – The Python Cryptography Toolkit PyCrypto, extended in PyCryptoDome
* keyczar – Cryptography Toolkit keyczar
* M2Crypto – M2Crypto is the most complete OpenSSL wrapper for Python.
* Cryptography – Python library which exposes cryptographic recipes and primitives.
* PyNaCl – Python binding for libSodium (NaCl)

Cryptography is a popular library and here is a basic example of how it works:
* ```python
  >>> import os
  >>> from cryptography.hazmat.primitives.ciphers.aead import AESCCM
  >>> data = b"a secret message"
  >>> aad = b"authenticated but unencrypted data"
  >>> key = AESCCM.generate_key(bit_length=128)
  >>> aesccm = AESCCM(key)
  >>> nonce = os.urandom(13)
  >>> ct = aesccm.encrypt(nonce, data, aad)
  >>> aesccm.decrypt(nonce, ct, aad)
  b'a secret message'
  ```
[Documentation](https://cryptography.io/en/latest/hazmat/primitives/aead/)


#### Java
Some of the popular libraries in Java:
* Java Cryptography Extension, integrated in the Java Runtime Environment since version 1.4.2
* IAIK JCE
* Bouncy Castle Crypto Library

An example from the Java Cryptographic Extensions:
* ```java
  SecretKey myKey = ...
  byte[] myAAD = ...
  byte[] plainText = ...
  int myTLen = ...
  byte[] myIv = ...

  GCMParameterSpec myParams = new GCMParameterSpec(myTLen, myIv);
  Cipher c = Cipher.getInstance("AES/GCM/NoPadding");
  c.init(Cipher.ENCRYPT_MODE, myKey, myParams);

  // AAD is optional, if present, it must be supplied before any update/doFinal calls.
  c.updateAAD(myAAD);  // if AAD is non-null
  byte[] cipherText = new byte[c.getOutputSize(plainText.length)];
  // conclusion of encryption operation
  int actualOutputLen = c.doFinal(plainText, 0, plainText.length, cipherText);

  // To decrypt, same AAD and GCM parameters must be supplied
  c.init(Cipher.DECRYPT_MODE, myKey, myParams);
  c.updateAAD(myAAD);
  byte[] recoveredText = c.doFinal(cipherText, 0, actualOutputLen);

  // MUST CHANGE IV VALUE if the same key were to be used again for encryption
  byte[] newIv = ...;
  myParams = new GCMParameterSpec(myTLen, newIv);
  ```
[WIKI PAGE WITH OTHER LANGUAGES](https://en.wikipedia.org/wiki/AES_implementations#Python)