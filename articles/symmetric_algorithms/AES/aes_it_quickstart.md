---
layout: quickstart
title: IT Admin's QuickStart
type: AES
qtype: it
upper-link: /articles/symmetric_algorithms/aes/aes.html
image: /img/common/pc-administrator.png
note: "An overview of where and how AES is often used in common IT applications such as the TLS module in Apache server and IPSec."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
alerts:

further-reading:

related-articles:

attacks:

---
<p id="GeneralAESInfo">

<h2> <img src="/img/common/configuration.jpg " style="width:110px;height:100px;" /> AES Configuration </h2>

<font size="4"><strong>What to expect:</strong></font><br /> <br />
For AES, the following configuration settings will provide the best possible security:
<ul>
<li>Enabling AES: The first step is to enable AES as an encryption scheme. This would also include making sure that any vulnerable/weak encryption algorithms are disabled accordingly.</li>
<li>Key Length: It is important that AES is deployed with a minimum key length of 128 bits. This is the minimum standard. As per NIST, 256-bit AES is good enough for TOP-SECRET traffic.</li>
<li>Mode of Operation: CTR or GCM. Choosing the right mode of operation is very important as it could not just effect security but also performance. </li>
</ul> <br /> <br />
<font size="4"><strong>Concept:</strong></font> AES is a <span class="green">recommended</span> encryption scheme by many security professionals and also US governmental agencies. This is because, it is considered to be almost unbreakable. There are a set of certain attacks that but they are not considered practical in the current time. It is , however, recommended to make sure that AES is properly configured.
<br /> <br /> <br />

<font size="3"><strong>Examples for Enabling AES:</strong></font> <br />
<br />We have categorized the examples into two sections. VPN and File Storage. These are the two section of usage where encryption is the most prevalent. <br />
<br />


<font size="3"><strong>Webservers: </strong></font> <br /> <br />
<ul>
<strong>Apache:</strong><br/> <br />

<pre>
<code>...
SSLProtocol ALL -SSLv2 -SSLv3
SSLCipherSuite ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:RSA+AESGCM:RSA+AES:!aNULL:!MD5:!DSS
...</code>
</pre>

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
<font size="3"><strong>VPN: </strong></font> <br />
We use the examples of TLSv1.2 and TLSv1.1 as our VPN protocols in the following examples here since they are the most secure at the moment. You can read more about why they are recommended <a href="/articles/cryptographic_protocols/tls-1-2.html">here</a>. TLS typically uses AES to encrypt data post the handshake completion. <br /> <br />
<ul>
<strong>Guide to reading cipher from configuration files: </strong><br /> <br />
One of the most popular formats look like this: <br />

<pre>
<code>...
ECDH+AESGCM:ECDH+AES256
...</code>
</pre>
<br />
The above example shows two cipher suites separated by a ':'. The first cipher 'ECDH+AESGCM' specifies ECDH as the signature algorithm for TLS while the AESGCM specifies the encryption scheme with its mode of operation. The second cipher, ECDH:AES256 specifies ECDH being used as the signature scheme and AES256 talks about the encryption algorithm. The mode of operation will be whatever is the system default. <br /> <br />
</ul>
</p>
