---
layout: quickstart
title: "Developer's QuickStart"
type: SHA1
qtype: dev
upper-link: /articles/hashing_algorithms/sha1.html
image: /img/common/NewDevLogo.png
note: "Are you a developer? Get started with crucial implementation details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
further-reading:
  - name: History of Hash Functions
    link: https://www.esat.kuleuven.be/cosic/publications/article-1532.pdf
  - name: Comparative Study Between MD5 and SHA-1
    link: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.659.1400&rep=rep1&type=pdf
  - name: Comparisons between the different SHAs
    link: https://en.wikipedia.org/wiki/Secure_Hash_Algorithms
---


### **Protocols Used In** 

* Transport Layer Security (TLS)
* Secure Sockets Layer (SSL)
* Pretty Good Privacy (PGP)
* Secure Shell (SSH)
* Secure/Multipurpose Internet Mail Extensions (S/MIME)
* Internet Protocol Security (IPSec)
<br /><br />

### **When and Where is SHA-1 Ok?**
Checking the hash of an executable or file that we know is trusted (from trusted site). No known flaws in SHA-1 as a key derivation function which is how dh-group14-sha1 is being used. Similarly, HMAC-SHA1 is believed to be (still) safe as long as SHA1 is pseudorandom. The specific construct of HMAC-SHA1 is still considered safe to use (assuming a secret key) due to the security proof for HMAC which does not rely on collision resistance of the underlying PRF.
<br /><br />

### **Simple Basic issues when doing web development and having or storing passwords using SHA-1.**
If you're a web developer, you've probably had to make a user account system. The most important aspect of a user account system is how user passwords are protected. User account databases are hacked frequently, so you absolutely must do something to protect your users' passwords if your website is ever breached. The best way to protect passwords is to employ salted password hashing. This page will explain why it's done the way it is.

The general workflow for account registration and authentication in a hash-based account system is as follows:

* The user creates an account.
* Their password is hashed and stored in the database. At no point is the plain-text (unencrypted) password ever written to the hard drive. 
* When the user attempts to login, the hash of the password they entered is checked against the hash of their real password (retrieved from the database).
* If the hashes match, the user is granted access. If not, the user is told they entered invalid login credentials.

Steps 3 and 4 repeat every time someone tries to login to their account. Refer to [Hashing page](example_index.html) for known Attacks on Hashes.
<br /><br />

### **Basic Implementation of SHA-1**
This is primarily for possible legacy device support. Ensure that this is done for less secure systems, and use stronger hashing for more secure systems.

#### In C/C++
1. 
  ```c
    #include <openssl/sha.h>
    int main()
    {  
      const char str[] = "Original String";
      unsigned char hash[SHA_DIGEST_LENGTH]; // == 20
      SHA1(str, sizeof(str) - 1, hash);
      // do some stuff with the hash
      return 0;
    }
  ```
OpenSSL crypto library: [https://www.openssl.org/docs/manmaster/man1/sha1.html](https://www.openssl.org/docs/manmaster/man1/sha1.html)\\
Man page: [https://www.openssl.org/docs/manmaster/crypto/sha.html](https://www.openssl.org/docs/manmaster/crypto/sha.html)<br /><br />
CryptoPP is a great C++ library for cryptographic functions. It has a method for calculating a SHA1 digest. See examples of the hashing functions [here](http://www.cryptopp.com/wiki/Hash_Functions).<br /><br />
Libcrypt: [http://www.gnupg.org/documentation/manuals/gcrypt/Available-hash-algorithms.html#Available-hash-algorithms](http://www.gnupg.org/documentation/manuals/gcrypt/Available-hash-algorithms.html#Available-hash-algorithms)<br /><br />
Another opensource library - Boost: [http://www.boost.org/doc/libs/1_46_0/libs/uuid/index.html](http://www.boost.org/doc/libs/1_46_0/libs/uuid/index.html)

2. 
  ```c
    // The data to be hashed
    char data[] = "Hello, world!";
    size_t length = sizeof(data);
    unsigned char hash[SHA_DIGEST_LENGTH];
    SHA1(data, length, hash);
    // hash now contains the 20-byte SHA-1 hash
    ++While using between packets in C:
    // Error checking omitted for expository purposes
    // Object to hold the current state of the hash
    SHA_CTX ctx;
    SHA1_Init(&ctx);
    // Hash each piece of data as it comes in:
    SHA1_Update(&ctx, "Hello, ", 7);
    ...
    SHA1_Update(&ctx, "world!", 6);
    // etc.
    ...
    // When you're done with the data, finalize it:
    unsigned char hash[SHA_DIGEST_LENGTH];
    SHA1_Final(hash, &ctx);
  ```

3. 
  ```c
    #include <openssl/sha.h>   
    int main(int argn, char *argv[]) {  
      int i = 0;
      unsigned char temp[SHA_DIGEST_LENGTH];
      char buf[SHA_DIGEST_LENGTH*2];
      if ( argn != 2 ) {
        printf("Usage: %s string\n", argv[0]);
        return -1;
      }
      memset(buf, 0x0, SHA_DIGEST_LENGTH*2);
      memset(temp, 0x0, SHA_DIGEST_LENGTH);
      SHA1((unsigned char *)argv[1], strlen(argv[1]), temp);
      for (i=0; i < SHA_DIGEST_LENGTH; i++) {
        sprintf((char*)&(buf[i*2]), "%02x", temp[i]);
      }
      printf("SHA1 of %s is %s\n", argv[1], buf);
      return 0;
    }
  ```
<br />

#### Compiling
* 
```ruby
$ gcc sha.c -lssl -o sha
$ ./sha asd
SHA1 of asd is f10e2821bbbea527ea02200352313bc059445190
```
<br />

#### In Python
* 
  ```python
    import hashlib
    hash_object = hashlib.sha1(b'Hello World')
    hex_dig = hash_object.hexdigest()
    print(hex_dig)

    import uuid
    import hashlib

    def hash_password(password):
        # uuid is used to generate a random number
        salt = uuid.uuid4().hex
        return hashlib.sha256(salt.encode() + password.encode()).hexdigest() + ':' + salt

    def check_password(hashed_password, user_password):
        password, salt = hashed_password.split(':')
        return password == hashlib.sha256(salt.encode() + user_password.encode()).hexdigest()

    new_pass = input('Please enter a password: ')
    hashed_password = hash_password(new_pass)
    print('The string to store in the db is: ' + hashed_password)
    old_pass = input('Now please enter the password again to check: ')
    if check_password(hashed_password, old_pass):
        print('You entered the right password')
    else:
        print('I am sorry but the password does not match')</code>
  ```