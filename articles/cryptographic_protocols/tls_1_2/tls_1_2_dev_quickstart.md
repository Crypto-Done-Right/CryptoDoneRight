---
layout: quickstart
title: "Developer's QuickStart"
type: TLS 1.2
qtype: dev
upper-link: /articles/cryptographic_protocols/tls_1_2/tls_1_2.html
image: /img/common/NewDevLogo.png
note: "Are you a developer? Get started with crucial implementation details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
alerts:
  - id: 1
    type: warning
    description: There are serious security implications if not configured properly!
    link: ""
  - id: 2
    type: success
    description: This is the RECOMMENDED standard.
    link: ""
further-reading:
  - name: "Python SSL/TLS Library"
    link: https://docs.python.org/2/library/ssl.html
  - name: "OWASP Cheat Sheet for TLS"
    link: https://www.owasp.org/index.php/Transport_Layer_Protection_Cheat_Sheet
  - name: "Book: Understanding SSL, TLS and PKI"
    link: https://www.feistyduck.com/books/bulletproof-ssl-and-tls/
  - name: "RFC for secure use of SSL, TLS and DTLS"
    link: https://datatracker.ietf.org/doc/rfc7525/?include_text=1
related-articles:
  - name: "RFC 5246: The Transport Layer Security (TLS) Protocol Version 1.2"
    link: https://tools.ietf.org/html/rfc5246
---

## <img src="/img/common/implementation.png " style="width:100px;height:100px;" /> TLS 1.2 Implementation

### **Concept**
DO NOT roll your own Crypto! Use standard services and libraries.

It is NOT advisable in any circumstances to develop any sort of cryptography on your own. Instead, there are a few options for standard libraries that can be used. These libraries offer better stability as they are usually a product of several years of experience in implementing cryptography by an active development community who are dedicated towards efforts in implementation. This constant review and improvement has characterized standard libraries as reliable and robust.
<br /><br />

#### Examples
OpenSSL is one such library which popular and therefore is used as an example for this concept. OpenSSL is not the only available crypto library. For a list of different libraries and a comparision between them, visit [here](https://en.wikipedia.org/wiki/Comparison_of_cryptography_libraries).

OpenSSL is a general purpose cryptography library that provides an open source implementation of the Secure Sockets Layer (SSL) and Transport Layer Security (TLS) protocols.

The library includes tools for generating RSA private keys, and Certificate Signing Requests (CSRs), checksums, managing certificates and performing encryption/decryption. OpenSSL is written in C, but wrappers are available for a wide variety of computer languages.

OpenSSL version 1.0.1 released on March 14, 2012 was the first OpenSSL Library to support TLSv1.2. But OpenSSL does not officially support the release anymore. Version 1.0.2 (released on 22nd January, 2015) is an Long Term Support (LTS) release and is scheduled to be supported till the end of year 2019. OpenSSL defines LTS support as follows:

* LTS releases will be supported for at least five years and we will specify one at least every four years. Non-LTS releases will be supported for at least two years.
* During the final year of support, we do not commit to anything other than security fixes. Before that, bug and security fixes will be applied as appropriate.

These are the official list of what is included in OpenSSL version 1.0.2:
* Suite B support for TLS 1.2 and DTLS 1.2
* Support for DTLS 1.2
* TLS automatic elliptic curve (EC) curve selection.
* API to set TLS supported signature algorithms and curves
* SSL_CONF configuration API.
* TLS Brainpool support.
* ALPN support.
* CMS support for RSA-PSS, RSA-OAEP, ECDH and X9.42 DH.

**Note:** [The latest major release for OpenSSL is 1.1.1 LTS](https://www.openssl.org/blog/blog/2018/09/11/release111/) (released on 11th September, 2018).. Again, we do not stress on upgrading OpenSSL blindly without properly evaluating the products that use them (and their advisories) and the consequences of an upgrade.

**Find out which openssl version you are using:**

Use the version option.

* ```ruby
  $ openssl version
  OpenSSL 1.0.1e-fips 11 Feb 2013
  ```

You can get much more information with the version -a option.

* ```ruby
  $ openssl version -a
  OpenSSL 1.0.1e-fips 11 Feb 2013
  built on: Thu Jul 23 19:06:35 UTC 2015
  platform: linux-x86_64
  options:  bn(64,64) md2(int) rc4(16x,int) des(idx,cisc,16,int)
            idea(int) blowfish(idx)
  compiler: gcc -fPIC -DOPENSSL_PIC -DZLIB -DOPENSSL_THREADS -D_REENTRANT
  -DDSO_DLFCN -DHAVE_DLFCN_H -DKRB5_MIT -m64 -DL_ENDIAN -DTERMIO
  -Wall -O2 -g -pipe -Wall -Wp,-D_FORTIFY_SOURCE=2 -fexceptions
  -fstack-protector --param=ssp-buffer-size=4 -m64 -mtune=generic
  -Wa,--noexecstack -DPURIFY -DOPENSSL_IA32_SSE2 -DOPENSSL_BN_ASM_MONT
  -DOPENSSL_BN_ASM_MONT5 -DOPENSSL_BN_ASM_GF2m -DSHA1_ASM -DSHA256_ASM
  -DSHA512_ASM -DMD5_ASM -DAES_ASM -DVPAES_ASM -DBSAES_ASM
  -DWHIRLPOOL_ASM -DGHASH_ASM
  OPENSSLDIR: "/etc/pki/tls"
  engines:  rdrand dynamic
  ```
<br />

## Usage of Cryptography in Programming Languages
### **Examples**
#### Python
There are a lot of libraries that Python can use for SSL/TLS. Some of the notable ones include the native SSL module in Python and PyOpenSSL. Both these libraries are essentially wrappers around the OpenSSL Library found on the system where Python is installed. Some behavior may be platform dependent, since calls are made to the operating system socket APIs. The installed version of OpenSSL may also cause variations in behavior.

To check which openssl version you are using execute the following within Python:
* ```python
  import ssl
  print ssl.OPENSSL_VERSION<
  ```
<br />

#### SSL library
Here is a basic example of how to use Python's SSL library to perform a TLS handshake using sockets:-

* ```java
  def handshake(sock):
    # this will trigger the handshake
    # if sock is already connected
    new_sock = ssl.wrap_socket(sock,
            ciphers="HIGH:-aNULL:-eNULL:-PSK:RC4-SHA:RC4-MD5",
            ssl_version=ssl.PROTOCOL_TLSv1_2,
        ...
        ...
            )
    return new_sock
  ```
<br />

#### pyOpenSSL library
pyOpenSSL is collaboratively developed by the Python Cryptographic Authority (PyCA) that also maintains the low-level bindings called cryptography. It's a well documented wrapper around OpenSSL and supports all the features required for TLSv1.2.

Almost everything that you would want with pyOpenSSL is on their website:\\
[https://pyopenssl.org/en/stable/](https://pyopenssl.org/en/stable/)

Here are some examples of opensource code that utilizes pyOpenSSL:\\
HTTP Server supporting SSL: [http://code.activestate.com/recipes/442473-simple-http-server-supporting-ssl-secure-communica/](http://code.activestate.com/recipes/442473-simple-http-server-supporting-ssl-secure-communica/)\\
HTTP Client: [http://www.de-brauwer.be/wiki/wikka.php?wakka=PyOpenSSLClient](http://www.de-brauwer.be/wiki/wikka.php?wakka=PyOpenSSLClient)\\
Validating a Certificate: [http://blog.san-ss.com.ar/2012/05/validating-ssl-certificate-in-python.html](http://blog.san-ss.com.ar/2012/05/validating-ssl-certificate-in-python.html)
<br /><br />

## <img src="/img/common/patch.png " style="width:100px;height:100px;" /> Upgrade/Patch Management

### **Concept**
<span class="red">Please be careful while upgrading your crypto library. Do not simply upgrade the package without thinking about the implications it might have on existing features of your application or operating system.</span>

A lot of application and Operating System vendors provide specific guidelines on how to upgrade your software. A lot of vendors perform extensive testing of new releases of libraries like OpenSSL to ensure that no existing functionality is affected. Usually, these vendors release their own updates called **backported packages**. The security team backports security fixes to the released code versions, so while you will not get new features you can be reasonably sure that your SSL libraries are up to date.

Here are a couple of examples for regarding upgrades to popular Operating Systems:\\
CentOS: [https://wiki.centos.org/PackageManagement/SourceInstalls](https://wiki.centos.org/PackageManagement/SourceInstalls)\\
RedHat: [https://access.redhat.com/security/updates/backporting/?sc_cid=3093](https://access.redhat.com/security/updates/backporting/?sc_cid=3093)

Certain advisories are usually posted when vulnerabilties are found in OpenSSL library, for example:\\
CentOS: [https://wiki.centos.org/Security/POODLE](https://wiki.centos.org/Security/POODLE)\\
RedHat: [https://access.redhat.com/articles/1232123](https://access.redhat.com/articles/1232123)