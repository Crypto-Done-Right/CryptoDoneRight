---
layout: quickstart
title: "Developer's QuickStart"
type: TLS 1.3
qtype: dev
upper-link: /articles/cryptographic_protocols/tls_1_3/tls_1_3.html
image: /img/common/NewDevLogo.png
note: "Examples on properly integrating TLSv1.3 into your application, with source code snippets in C and python."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
alerts:
  - id: 1
    type: warning
    description: "Background Reading: Understanding Different Types of Problems in Crypto."
    link: "/flaw_categories.html"
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
  - name: "RFC 8446: The Transport Layer Security (TLS) Protocol Version 1.3"
    link: https://tools.ietf.org/html/rfc8446

---
<p id="nocryptoroll">
  <div class="col-md-12 col-sm-12 col-xs-12">

<h2> <img src="/img/common/patch.png " style="width:100px;height:100px;" /> Upgrade/Patch Management </h2>

<font size="4"><strong>Concept:</strong></font>  DO NOT roll your own Crypto! Use standard services and libraries. <br />

It is NOT advisable in any circumstances to develop any sort of cryptography on your own. Instead, there are a few options of standard libraries that can be used.
These libraries offer better stability as they are usually a product of several years of experience in implementing cryptography by an active development community who are
dedicated towards efforts in implementation. It is therefore considered to be reliable and robust. <br /> <br />


<font size="3"><strong>Examples:</strong></font>
Openssl is one such library which popular and therefore is used as an example for this concept.
OpenSSL is not the only available crypto library. For a list of different libraries and a comparision
between them, visit <a href="https://en.wikipedia.org/wiki/Comparison_of_cryptography_libraries">here</a>.
<br /> <br />

OpenSSL is a general purpose cryptography library that provides an open source implementation of the Secure Sockets Layer (SSL) and Transport Layer Security (TLS) protocols.
<br /> <br />
The library includes tools for generating RSA private keys and Certificate Signing Requests (CSRs), checksums, managing certificates and performing encryption/decryption. OpenSSL is written in C, but wrappers are available for a wide variety of computer languages.
<br /> <br />

<font sixe = "2"><strong> Which version of OpenSSL do I upgrade to? </strong></font><br />
OpenSSL version 1.0.1 released on March 14, 2012 was the first OpenSSL Library to support TLSv1.2. But OpenSSL does not officially support the release anymore. Version 1.0.2 (released on 22nd January, 2015) is an LTS release and is scheduled to be supported till the end of year 2019. OpenSSL defines LTS support as follows:

<ul>
<li>LTS releases will be supported for at least five years and we will specify one at least every four years. Non-LTS releases will be supported for at least two years.</li>
<li>During the final year of support, we do not commit to anything other than security fixes. Before that, bug and security fixes will be applied as appropriate.</li>
</ul>

<br /> <br />
These are the official list of what is included in OpenSSL version 1.0.2: <br /> <br />
<ul>
<li>Suite B support for TLS 1.2 and DTLS 1.2</li>
<li>Support for DTLS 1.2</li>
<li>TLS automatic elliptic curve (EC) curve selection.</li>
<li>API to set TLS supported signature algorithms and curves</li>
<li>SSL_CONF configuration API.</li>
<li>TLS Brainpool support.</li>
<li>ALPN support.</li>
<li>CMS support for RSA-PSS, RSA-OAEP, ECDH and X9.42 DH.</li>
</ul> <br />
<b>Note:</b> <a href="https://www.openssl.org/blog/blog/2018/09/11/release111/">The latest major release for OpenSSL is 1.1.1 LTS (released on 11th September, 2018).</a>. Again, we do not stress on upgrading OpenSSL blindly without properly evaluating the products that use them (and their advisories) and the consequences of an upgrade.
<br /><br />
<strong>Find out which openssl version you are using</strong>:
<br /><br />
Use the version option.
<br /><br />
<pre>
<code>$ openssl version
OpenSSL 1.0.1e-fips 11 Feb 2013</code></pre>

<br /> <br />
You can get much more information with the version -a option.
<pre>
<code>$ openssl version -a
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
</code>
</pre>
<br />
<font size="4"><strong>Concept:</strong></font> <span class="red">Please be careful while upgrading your crypto library. Do not simply upgrade the package without thinking about the implications it might have on existing features of your application or operating system. </span> <br />
<br />
A lot of application and Operating System vendors provide specific guidelines on how to upgrade your software. These vendors perform extensive testing of new releases of
libraries like OpenSSL to ensure that no existing functionality is affected. Usually, these vendors release their own updates called <strong>backported packages</strong>. The security team
backports security fixes to the released code versions, so while you will not get new features you can be reasonably sure that your SSL libraries are up to date.
<br />
Here are a couple of examples for regarding upgrades to popular Operating Systems: <br />
CentOS: <a href="https://wiki.centos.org/PackageManagement/SourceInstalls">https://wiki.centos.org/PackageManagement/SourceInstalls </a><br />
RedHat: <a href="https://access.redhat.com/security/updates/backporting/?sc_cid=3093"> https://access.redhat.com/security/updates/backporting/?sc_cid=3093 </a><br /> <br />

Certain advisories are usually posted when vulnerabilties are found in OpenSSL library, for example: <br />
CentOS: <a href="https://wiki.centos.org/Security/POODLE">https://wiki.centos.org/Security/POODLE </a><br />
RedHat: <a href="https://access.redhat.com/articles/1232123">https://access.redhat.com/articles/1232123 </a><br /> <br />


<p id="usagelibrary">

<h2>Upgrade to secure SSL/TLS in Programming Languages</h2>

<font size="4"><strong>Concept:</strong></font> It is again advised to not roll out your own cryptography while developing software. There are popular libraries in almost all programming
languages that can readily be used to perform cryptographic operations.
<br /> <br />
<font size="4"><strong>Examples:</strong></font> <br />
<strong>Python </strong> <br />
There are a lot of libraries that Python can use for SSL/TLS. Some of the notable ones include the native SSL module in Python and PyOpenSSL. Both these libraries are essentially wrappers around the OpenSSL Library found on the system where Python is installed. Some behavior may be platform dependent, since calls are made to the operating system socket APIs. The installed version of OpenSSL may also cause variations in behavior.
<br /> <br />
To check which openssl version you are using execute the following within Python:
<pre>
<code>import ssl
print ssl.OPENSSL_VERSION</code></pre>

<br />

<strong>ssl library</strong> <br /> <br />
Here is a basic example of how to use Python's SSL library to perform a TLSv1.2 handshake using sockets. If you are using <i>ssl</i> library in your application, look for the following code block and adjust the parameters accordingly.

<pre>
<code>def handshake(sock):
# this will trigger the handshake
# if sock is already connected
new_sock = ssl.wrap_socket(sock,
        ciphers="HIGH:-aNULL:-eNULL:-PSK:RC4-SHA:RC4-MD5",
        ssl_version=ssl.PROTOCOL_SSLv3,
		...
		...
        )
return new_sock</code>
</pre>

For TLSv1.2, a small change in the above would be to have

<pre>
<code>ssl_version=ssl.PROTOCOL_TLSv1_2</code></pre>


<strong>pyopenssl library</strong> <br /> <br />
pyOpenSSL is collaboratively developed by the Python Cryptography Authority (PyCA) that also maintains the low-level bindings called cryptography. It's a well documented wrapper around OpenSSL and supports all the features required for TLSv1.2 and more details <a href="https://pyOpenSSL.org/en/stable/api/crypto.html">here</a>.  <br /> <br />

Almost everything that you would want with pyOpenSSL is on their website:  <br />
<a href="https://pyopenssl.org/en/stable/">https://pyopenssl.org/en/stable/ </a><br /> <br />

Here are some examples of opensource code that utilizes pyOpenSSL: <br />
HTTP Server supporting SSL: <a href="http://code.activestate.com/recipes/442473-simple-http-server-supporting-ssl-secure-communica/"> http://code.activestate.com/recipes/442473-simple-http-server-supporting-ssl-secure-communica/ </a> <br />
HTTP Client: <a href="http://www.de-brauwer.be/wiki/wikka.php?wakka=PyOpenSSLClient">http://www.de-brauwer.be/wiki/wikka.php?wakka=PyOpenSSLClient </a><br />
Validating a Certificate: <a href="http://blog.san-ss.com.ar/2012/05/validating-ssl-certificate-in-python.html"> http://blog.san-ss.com.ar/2012/05/validating-ssl-certificate-in-python.html </a><br />
</p><br /><br />
