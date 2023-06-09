---
layout: quickstart
title: "Developer's QuickStart"
type: AES-CTR
qtype: dev
upper-link: /articles/symmetric_algorithms/mode_ctr/mode_ctr.html
image: /img/common/NewDevLogo.png
note: "Are you a developer? Get started with crucial implementation details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
alerts:

further-reading:
  - name: AES Encryption and Decryption in Java(CBC Mode)
    link: http://www.devglan.com/corejava/java-aes-encypt-decrypt

related-articles:
  - name: AES in IoT
    link: http://ardiri.com/blog/utls_defining_lightweight_security_for_iot_part_5

attacks:
---
## <img src="/img/common/configuration.jpg " style="width:110px;height:100px;" /> AES CTR Mode

**Why CTR Mode**\\
Considered a safe and efficient method of operation. Both CBC and CTR come recommended by Niels Ferguson and Bruce Schneier, both of whom are respected cryptographers.

**How it works**\\
This essentially involves encrypting a sequence of incrementing numbers prefixed with a nonce (number used once) to produce a keystream, and again is a stream cipher mode.

**Where is it commonly used**\\
CTR is used in many of the SSL/TLS cipher suites.

**How to use CTR**
* aes-128-ctr ← this is okay
* aes-192-ctr
* aes-256-ctr ← this is recommended

CTR mode is widely accepted and any problems are considered a weakness of the underlying block cipher, which is expected to be secure regardless of systemic bias in its input.

**How secure**

<span class="red">CTR requires no padding </span>

CTR mode is special in a few ways:

*  Padding doesn't apply and therefore eliminates all the padding attacks that were possible with modes like CCB where padding is required. . Normally, a block encryption algorithm (AES, Blowfish, DES, RC2, etc.) emit encrypted output that is a multiple of the block size (16 bytes for AES as an example). With CTR mode, the number of bytes output is exactly equal to the number of bytes input, so no padding/unpadding is required. The PaddingScheme property does not apply for counter mode.
* CTR mode increments a counter for each subsequent block encrypted. For example, if an application encrypted the string "1234567890" twenty times in a row, using the same instance of the Chilkat Crypt2 object, then each iteration's result would be different. This is because the counter is being incremented. The decrypting application would need to decrypt in exactly the same manner. The 1st decrypt should begin with a new instance of a Crypt2 object so that it's counter is at the initial value of 0.

It would be a mistake to encrypt 20 strings using an instance of the Crypt2 object, and then attempt to decrypt with the same Crypt2 object. To decrypt successfully, the app would need to instantiate a new Crypt2 object and then decrypt, so that the counters match.

<span class="green">Good points:</span>  Secure when done right, parallel encryption and decryption.\\
<span class="red">Bad points:</span>  Not many. Some question the security of the "related plaintext" model but it's generally considered to be safe.

## <img src="/img/common/implementation.png " style="width:100px;height:100px;" /> AES Implementation

### **Concept**
DO NOT roll your own Crypto! Use standard services and libraries.

It is NOT advisable in any circumstances to develop any sort of cryptography on your own. Instead , there are a few options for standard libraries that can be used. These libraries offer better stability as they are usually a product of several years of experience in implementing cryptography by an active development community who are dedicated towards efforts in implementation. It is therefore considered to be reliable and robust.


#### Examples
OpenSSL is one such library which popular and therefore is used as an example for this concept. OpenSSL is not the only available crypto library. For a list of different libraries and a comparision between them, visit [here](https://en.wikipedia.org/wiki/Comparison_of_cryptography_libraries).

The recommended version of OpenSSL that is to be used for AES is 1.1.0. This is for various reasons that concern and do not concern with AES. Some of them include for the latest encryption standards and removal of older vulnerable ones.
<br /><br />

## Usage of Cryptography in Programming Languages

### **Concept**
It is again advised to not roll out your own cryptography while developing software. There are popular libraries in almost all programming languages that can readily be used to perform cryptographic operations.
<br /><br />

### Examples
#### PHP
Examples of encryption and decryption  using AES in PHP:

[https://askubuntu.com/questions/60712/how-do-i-quickly-encrypt-a-file-with-aes](https://askubuntu.com/questions/60712/how-do-i-quickly-encrypt-a-file-with-aes)

#### Java

Example:
  * ```java
    /**
    Copyright (c) 2013 The University of Texas at Dallas, Data Security and Privacy Lab.
    All rights reserved.
    
    Licensed under the Apache License, Version 2.0 (the "License"); you may not use this
    file except in compliance with the License. You may obtain a copy of the License at
    
    http://www.apache.org/licenses/LICENSE-2.0.html
    
    Unless required by applicable law or agreed to in writing, software distributed
    under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR
    CONDITIONS OF ANY KIND, either express or implied. See the License for the specific
    language governing permissions and limitations under the License. See accompanying
    LICENSE file.
    */

    package edu.utdallas.bigsecret.cipher;

    import java.math.BigInteger;
    import java.security.SecureRandom;

    import javax.crypto.spec.IvParameterSpec;
    import javax.crypto.spec.SecretKeySpec;

    import org.apache.commons.lang.ArrayUtils;


    /**
    * This class extends abstract Cipher class. It implements AES in counter mode.
    */
    public class AesCtr extends JavaxCipher
    {
        /**
          * Secure random generator.
          */
        protected SecureRandom m_secureRandom;

        /**
          * Number of bytes in a block, which is constant for AES.
          */
        protected static int BLOCK_SIZE_BYTES = 16;

        /**
          * Number of bits in a block, which is constant for AES.
          */
        protected static int BLOCK_SIZE_BITS = 128;

        /**
          * Number of bytes in key.
          */
        protected int KEY_SIZE_BYTES;


        /**
          * Class constructor. Creates a Javax.Crypto.Cipher instance with AES in CTR<br />
          * mode, without any padding.
          * @param key Input key for the cipher. Should be 16, 24, or 32 bytes long
          * @throws Exception Throws exception if key length is not 16, 24, or 32 bytes.<br />
          *       May throw exception based on Javax.Crypto classes.
          */
        public AesCtr(byte[] key) throws Exception
        {
            //use default constructor for cipher.Cipher
            super();

            //check if input key is ok
            if(key.length != 16 && key.length != 24 && key.length != 32)
            {
                throw new Exception("Key length should be 16, 24, or 32 bytes long");
            }

            //set key length
            KEY_SIZE_BYTES = key.length;

            //create secret key spec instance
            m_keySpec = new SecretKeySpec(key, "AES");

            //create cipher instance
            m_cipher = javax.crypto.Cipher.getInstance("AES/CTR/NoPadding");

            //create secure random number generator instance
            m_secureRandom = new SecureRandom();
        }


        /**
          * Encrypts input data with AES CTR mode.
          * @param data Input byte array.
          * @return Encryption result.
          * @throws Exception Throws exception if there is no data to encrypt.<br />
          *       May throw exception based on Javax.Crypto.Cipher class
          */
        public byte[] encrypt(byte[] data) throws Exception
        {
            //check if there is data to encrypt
            if(data.length == 0)
            {
                throw new Exception("No data to encrypt");
            }

            //create iv
            byte[] iv = new byte[BLOCK_SIZE_BYTES];
            byte[] randomNumber = (new BigInteger(BLOCK_SIZE_BITS, m_secureRandom)).toByteArray();
            int a;
            for(a = 0; a<randomNumber.length && a<BLOCK_SIZE_BYTES; a++)
            iv[a] = randomNumber[a];
            for(; a<BLOCK_SIZE_BYTES; a++)
            iv[a] = 0;

            //init cipher instance
            m_cipher.init(javax.crypto.Cipher.ENCRYPT_MODE, m_keySpec, new IvParameterSpec(iv));

            //return concatenation of iv + encrypted data
            return ArrayUtils.addAll(iv, m_cipher.doFinal(data));
        }


        /**
          * Decrypts input data with AES CTR mode
          * @param data Input byte array.
          * @return Decryption result.
          * @throws Exception Throws exception if there is no data to decrypt.<br />
          *       May throw exception based on Javax.Crypto.Cipher class.
          */
        public byte[] decrypt(byte[] data) throws Exception
        {
            //call overriden function with offset = 0
            return decrypt(data, 0);
        }


        /**
          * Decrypts input data starting and including the offset index position<br />
          * with AES CTR mode.
          * @param data Input byte array.
          * @param offset Offset to start decryption.
          * @return Decryption result.
          * @throws Exception Throws exception if there is no data to decrypt.<br />
          *       Throws exception if offset is invalid.<br />
          *       May throw exception based on Javax.Crypto.Cipher class.
          */
        public byte[] decrypt(byte[] data, int offset) throws Exception
        {
            //check if there is data to decrypt after the offset and iv
            if(data.length <= BLOCK_SIZE_BYTES + offset)
            {
                throw new Exception("No data to decrypt");
            }

            //get iv value from the beggining of data
            byte[] iv = new byte[BLOCK_SIZE_BYTES];
            System.arraycopy(data, offset, iv, 0, BLOCK_SIZE_BYTES);

            //init cipher instance
            m_cipher.init(javax.crypto.Cipher.DECRYPT_MODE, m_keySpec, new IvParameterSpec(iv));

            //return decrypted value
            return m_cipher.doFinal(data, (BLOCK_SIZE_BYTES + offset), data.length - (BLOCK_SIZE_BYTES + offset));
        }
    }
    ``` 