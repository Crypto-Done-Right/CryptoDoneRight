---
layout: quickstart
title: "Developer's QuickStart"
type: AES-CBC
qtype: dev
upper-link: /articles/symmetric_algorithms/mode_cbc/mode_cbc.html
image: /img/common/NewDevLogo.png
note: "Are you a developer? Get started with crucial implementation details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
alerts:
  - id: 1
    type: warning
    description: "Background Reading: Understanding Different Types of Problems in Crypto."
    link: "/flaw_categories.html"
further-reading:
related-articles:
attacks:
---
## <img src="/img/common/configuration.jpg " style="width:110px;height:100px;" /> AES CBC Introduction

**Why CBC Mode**\\
CBC - Cipher Block Chaining. This mode is very common, and is considered to be reasonably secure.

**How it works**\\
Each block of plaintext is xor'ed with the previous block of ciphertext before being transformed, ensuring that identical plaintext blocks don't result in identical ciphertext blocks when in sequence. For the first block of plaintext (which doesn't have a preceding block) we use an initialization vector instead. This value should be unique per message per key, to ensure that identical messages don't result in identical ciphertexts.

**Where is it commonly used**\\
CBC is used in many of the SSL/TLS cipher suites.

**How secure**\\
Unfortunately, there are attacks against CBC when it is not implemented alongside a set of strong integrity and authenticity checks. One property it has is block-level malleability, which means that an attacker can alter the plaintext of the message in a meaningful way without knowing the key, if he can mess with the ciphertext. As such, implementations usually include a HMAC-based authenticity record. But we are going to save that for a later post.

**How to use it securely**
* Ensure you are using a randomized IV that is not re-used.
* Use PKCS7 padding: Normally, a block encryption algorithm (AES, Blowfish, DES, RC2, etc.) emit encrypted output that is a multiple of the block size (16 bytes for AES as an example). This is only required in CBC mode. In CTR mode, the number of bytes output is exactly equal to the number of bytes input, so no padding/unpadding is required.
* For all the recommendations, please follow the FAQ page on the landing page.

**What to use**\\
These are the most commonly available options:

aes-128-cbc ← this is okay\\
aes-192-cbc\\
aes-256-cbc ← this is recommended

<span class="green">Good points:</span>  Secure when used properly, parallel decryption.\\
<span class="red">Bad points:</span>  No parallel encryption, susceptible to malleability attacks when authenticity checks are bad / missing. But when done right, it's very good.

## <img src="/img/common/implementation.png" style="width:100px;height:100px;" /> AES Implementation

### **Concept**
DO NOT roll your own Crypto! Use standard services and libraries.

It is NOT advisable in any circumstances to develop any sort of cryptography on your own. Instead , there are a few options for standard libraries that can be used. These libraries offer better stability as they are usually a product of several years of experience in implementing cryptography by an active development community who are dedicated towards efforts in implementation. It is therefore considered to be reliable and robust.

#### Examples
OpenSSL is one such library which popular and therefore is used as an example for this concept.
OpenSSL is not the only available crypto library. For a list of different libraries and a comparision
between them, visit [here](https://en.wikipedia.org/wiki/Comparison_of_cryptography_libraries).

The recommended version of OpenSSL that is to be used for AES is 1.1.0. This is for various reasons that concern and do not concern with AES. Some of them include for the latest encryption standards and removal of older vulnerable ones.

To use openssl:

Encryption:\\
``` openssl aes-256-cbc -in attack-plan.txt -out message.enc```

Decryption:\\
``` openssl aes-256-cbc -d -in message.enc -out plain-text.txt```

You can get openssl to base64-encode the message by using the -a switch on both encryption and decryption. This way, you can paste the ciphertext in an email message, for example. It'll look like this:
* ```ruby
  $ openssl aes-256-cbc -in attack-plan.txt -a
  enter aes-256-cbc encryption password:
  Verifying - enter aes-256-cbc encryption password:
  U2FsdGVkX192dXI7yHGs/4Ed+xEC3ejXFINKO6Hufnc=
  ```

Note: OpenSSL uses PKCS7 by default for padding.

## Usage of Cryptography in Programming Languages
### **Concept**
It is again advised to not roll out your own cryptography while developing software. There are popular libraries in almost all programming languages that can readily be used to perform cryptographic operations.

### **Examples**
#### PHP
Examples of encryption and decryption  using AES in PHP:\\
[https://askubuntu.com/questions/60712/how-do-i-quickly-encrypt-a-file-with-aes](https://askubuntu.com/questions/60712/how-do-i-quickly-encrypt-a-file-with-aes)

#### Java
<span class="green">AES Encryption in Java</span>

Following is the sample program in Java that performs AES encryption. Here, we are using AES with CBC mode to encrypt a message as ECB mode is not semantically secure.The IV (what is an IV? <!--LINK HERE-->) mode should also be randomized for CBC mode. And the mode of padding is PKCS7. <!--WHAT and WHY PKCS7--> 

If the same key is used to encrypt all the plain text and if an attacker finds this key then all the cipher can be decrypted in the similar way.We can use salt and iterations to improve the encryption process further.In the following example we are using 128 bit encryption key.

An Example:
  * ```java
    private static final String key = "aesEncryptionKey";
    private static final String initVector = "encryptionIntVec";

    public static String encrypt(String value) {
        try {
            IvParameterSpec iv = new IvParameterSpec(initVector.getBytes("UTF-8"));
            SecretKeySpec skeySpec = new SecretKeySpec(key.getBytes("UTF-8"), "AES");

            Cipher cipher = Cipher.getInstance("AES/CBC/PKCS5PADDING");
            cipher.init(Cipher.ENCRYPT_MODE, skeySpec, iv);

            byte[] encrypted = cipher.doFinal(value.getBytes());
            return Base64.encodeBase64String(encrypted);
        } catch (Exception ex) {
            ex.printStackTrace();
        }
        return null;
    }
  ```

<span class="red">AES Decryption in Java</span>

Following is the reverse process to decrypt the cipher.The code is self explanatory.

  * ```java
    public static String decrypt(String encrypted) {
        try {
            IvParameterSpec iv = new IvParameterSpec(initVector.getBytes("UTF-8"));
            SecretKeySpec skeySpec = new SecretKeySpec(key.getBytes("UTF-8"), "AES");

            Cipher cipher = Cipher.getInstance("AES/CBC/PKCS7PADDING");
            cipher.init(Cipher.DECRYPT_MODE, skeySpec, iv);
            byte[] original = cipher.doFinal(Base64.decodeBase64(encrypted));

            return new String(original);
        } catch (Exception ex) {
            ex.printStackTrace();
        }

        return null;
    }

    // Testing AES Encryption and Decryption
    // Following is the main() implementation to test our AES implementation.

    public static void main(String[] args) {
        String originalString = "password";
        System.out.println("Original String to encrypt - " + originalString);
        String encryptedString = encrypt(originalString);
        System.out.println("Encrypted String - " + encryptedString);
        String decryptedString = decrypt(encryptedString);
        System.out.println("After decryption - " + decryptedString);
    }
  ```