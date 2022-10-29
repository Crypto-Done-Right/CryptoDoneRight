---
layout: quickstart
title: IT Admin's QuickStart
type: AES-CBC
qtype: it
upper-link: /articles/symmetric_algorithms/mode_cbc/mode_cbc.html
image: /img/common/pc-administrator.png
note: "Are you an IT administrator? Get started with best practice setup details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks

alerts:
  - id: 1
    type: warning
    description: "Background Reading: Understanding Different Types of Problems in Crypto."
    link: "/flaw_categories.html"
---

<p id="GeneralAESInfo">

<h2> <img src="/img/common/configuration.jpg " style="width:110px;height:100px;" /> AES CBC Introduction </h2>

<font size="3"><strong>How it works: </strong></font><br />
Each block of plaintext is xor'ed with the previous block of ciphertext before being transformed, ensuring that identical plaintext blocks don't result in identical ciphertext blocks when in sequence. For the first block of plaintext (which doesn't have a preceding block) we use an initialization vector instead. This value should be unique per message per key, to ensure that identical messages don't result in identical ciphertexts. <br /> <br />

<strong>Where is it commonly used:</strong><br />
CBC is used in many of the SSL/TLS cipher suites. AES in CBC modes can also be used for file storage. <br /> <br />

<strong>Current Digital Cryptography Requirements</strong> <br />
In today's electronic age, the importance of digital cryptography in securing electronic data transactions is unquestionable. Every day, users electronically generate and communicate a large volume of information with others. This information includes medical, financial and legal files; automatic and Internet banking; phone conversations; pay-per-view television; and other e-commerce transactions. The following examples, as well as many other applications, require a great deal of security in the storage and transportation of this information. By using various digital-cryptography techniques, people and organizations can secure electronic information to protect economic interests, prevent fraud, and guarantee the privacy of individuals. <br /><br />

<strong>Voice Communications</strong><br />
There is a potentially significant market for high-strength encryption on VoIP, wireless phone, and land-line phone communications. The perceived threat of eavesdropping is a powerful market driver in the world of personal communications. Expect Nokia, Ericsson, Samsung, Motorola, TI, Casio, and the other major phone makers to move in, along with a cadre of startups that hope to provide the IP. Once one major vendor offers encryption on a popular phone then, rapidly, every other vendor will be forced to follow suit or lose business to competition. In the space of 18-24 months, encryption mode will become the default talk mode. Expect every VoIP system and land-line phone to gain this functionality as well.<br /><br />


<strong>Network Appliances</strong><br />
Another potentially large market for digital encryption is network appliances—anything electronic that is interactively hooked up to a network. As the number of non-PC and wireless devices accessing the Internet increases, the rate of cyber attacks on network infrastructure and service providers will increase. Critical functions such as power-grid management and water-distribution systems are shifting to the Web and need to be protected. Even simple appliances such as fire alarms or temperature alarms can be vulnerable to hacker attacks. There is great value in preventing a hacker from electronically yelling, "fire".<br /><br />


<strong>Virtual Private Network (VPN)</strong><br />
VPNs protect direct connections between users and enterprise networks. The high cost of dedicated telecom links compels transition from software to hardware support for these links. Dedicated lease lines are relatively private and secure, but it's too expensive to give everyone a private line. Putting encrypted VPN traffic on public lines is less expensive. While few individual users require a dedicated connection at Gbit/sec speeds, the ballooning number of VPN users means a corporate LAN will need to aggregate and process encrypted data streams in the gigabit range now, and in the multi-gigabit range in the near future.<br /><br />


<strong>Secure Socket Layer (SSL)</strong><br />
SSLs provide security using the Secure Socket Layer protocol for Internet browser-based transactions (in other words, SSL is Web specific). The presence of encryption on a Web site is often the deciding factor whether to make an online transaction; no company wants to lose business for lack of a secure connection. As bandwidth requirements go up, it is vital to include a resident SSL hardware accelerator in the data center to encode and decode traffic going in and out of the Web site.<br /><br />

Note that SSL processing currently works from a suite of algorithms including DES, 3-DES, IDEA, RC-2, and RC-4 (plus digital signature algorithms such as SHA and MD5). It is too early to tell whether AES will simply be added to SSL ciphers or used to replace the other algorithms altogether. It is important to realize that the NIST (National Institute of Standards and Technology) selection team decided against a multiple-algorithm AES. One of the primary reasons is that multiple AES key sizes provide increased levels of security. Another primary reason is that a single-algorithm AES decreases the complexity of implementations that will be built to comply with the AES specifications, thereby lowering costs and promoting interoperability.<br /><br />

<strong>Why CBC Mode?</strong><br />
CBC - Cipher Block Chaining. This mode is very common, and is considered to be reasonably secure.  <br /> <br />

<strong>How secure?</strong><br />
Unfortunately, there are attacks against CBC when it is not implemented alongside a set of strong integrity and authenticity checks. One property it has is block-level malleability, which means that an attacker can alter the plaintext of the message in a meaningful way without knowing the key, if he can mess with the ciphertext. As such, implementations usually include a HMAC-based authenticity record. But we are going to save that for a later post. <br /> <br />

<strong>How to use it securely:</strong><br />
<ul>
<li>Ensure you are using a randomized IV that is not re-used.</li>
<li>Use PKCS7 padding: Normally, a block encryption algorithm (AES, Blowfish, DES, RC2, etc.) emit encrypted output that is a multiple of the block size (16 bytes for AES as an example). This is only required in CBC mode. In CTR mode, the number of bytes output is exactly equal to the number of bytes input, so no padding/unpadding is required.</li>
<li>For all the recommendations, please follow the FAQ page on the landing page. </li>
</ul>

<strong>What to use:</strong><br />
These are the most commonly available options: <br /> <br />

aes-128-cbc ← this is okay <br />
aes-192-cbc <br />
aes-256-cbc ← this is recommended <br /> <br />

<font size="3"><strong>Webservers: </strong><font size="3"> <br /> <br />
<ul>
<strong>Apache: </strong> <br/> <br />
The main configuration file is usually called httpd.conf. The location of this file is set at compile-time, but may be overridden with the -f command line flag.

By default, the configuration file is named nginx.conf and placed in the directory /usr/local/nginx/conf , /etc/nginx , or /usr/local/etc/nginx.

<pre>
<code>...
SSLProtocol ALL -SSLv2 -SSLv3
SSLCipherSuite ECDH+AESCBC:DH+AESCBC:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:RSA+AESCBC:RSA+AES:!aNULL:!MD5:!DSS
...</code>
</pre>

The above list showcases a bunch of ciphers which will be supported over TLS. All these cipher suites are separated by a ':'. For example,

<pre>
  <code>
    ECDH+AESGCM:ECDH+AES256
  </code>
</pre>

The above example shows two cipher suites separated by a ':'. The first cipher 'ECDH+AESGCM' specifies ECDH as the signature algorithm for TLS while the AESGCM specifies the encryption scheme with its mode of operation. The second cipher, ECDH:AES256 specifies ECDH being used as the signature scheme and AES256 talks about the encryption algorithm. The mode of operation will be whatever is the system default. <br /> <br />

This works on both Apache 2.2 and 2.4. If your OpenSSL doesn’t support the preferred modern ciphers (like the still common 0.9.8), it will fall back gracefully but your configuration is ready for the future.<br /> <br />

<strong> Nginx: </strong> <br /> <br />
By default, the configuration file is named nginx.conf and placed in the directory /usr/local/nginx/conf , /etc/nginx , or /usr/local/etc/nginx.
<br /> <br />
<pre>
<code>...
ssl_protocols TLSv1 TLSv1.1 TLSv1.2;
ssl_ciphers ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:RSA+AESGCM:RSA+AES:!aNULL:!MD5:!DSS;
...</code>
</pre> <br /> <br />
</ul>
<font size="3"><strong>VPN: </strong><font size="3"> <br />
We use the examples of TLSv1.2 and TLSv1.1 as our VPN protocols in the following examples here since they are the most secure at the moment. You can read more about why they are recommended here <a href="articles/cryptographic_protocols/tls/tls_1_2.md">here</a>. TLS uses AES to encrypt data post the handshake completion. <br /> <br />

<strong>Guide to reading cipher from configuration files: </strong><br /> <br />
One of the most popular formats look like this: <br />

<pre>
<code>...
ECDH+AESGCM:ECDH+AES256
...</code>
</pre>
<br />
The above example shows two cipher suites separated by a ':'. The first cipher 'ECDH+AESGCM' specifies ECDH as the signature algorithm for TLS while the AESGCM specifies the encryption scheme with its mode of operation. The second cipher, ECDH:AES256 specifies ECDH being used as the signature scheme and AES256 talks about the encryption algorithm. The mode of operation will be whatever is the system default.
