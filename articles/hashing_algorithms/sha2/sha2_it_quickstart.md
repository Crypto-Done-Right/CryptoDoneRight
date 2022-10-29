---
layout: quickstart
title: "IT Admin's QuickStart"
type: SHA2
qtype: it
upper-link: /articles/hashing_algorithms/sha2.html
image: /img/common/NewDevLogo.png
note: "Are you an IT administrator? Get started with best practice setup details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks

---
<p id="GeneralInfo">

<h2> <img src="/img/common/configuration.jpg " style="width:110px;height:100px;" /> SHA2 Configuration </h2>

<font size="4"><strong>What to expect:</strong></font><br /> <br />
SHA2 can be utilized in several applications in your IT infrastructure. Here are some of the examples:
<ul>
<li>VPN: Message integrity is one of the security features of VPN. This could be provided by SHA2. All VPN protocols are handshake protocols and therefore an exchange of messages decide which encryption and hashing algorithms are selected for security.
</li>
<li>Digital Signatures: SHA2 is also used in digital certificates in "Digital Signatures". Your digital certificates could be used in VPN protocols or while serving a website from a server.</li>
<li>Store Passwords: Passwords are never stored in plain text in a database for security reasons. Instead, hash of the passwords are stored. The algorithm that generates the hashes is therefore important too.</li>
<br />
For the above settings, there have been examples mentioned below.
</ul> <br /> <br />
<font size="4"><strong>Concept:</strong></font> SHA2 is one of the recommended options for hashing. This is because there have been no security problems found in the protocol so far. Translating that to more technical terms, there hasn't been a collision found yet. It has to be ensured that all applications in your infrastructure run SHA2 at the least (among the SHA family).  
<br /> <br />

<font size="3"><strong>Examples for Enabling SHA2 for VPN/HTTPS connections	</strong></font> <br />
<br />We have categorized the examples into two sections:- Webservers and Browsers. <br />
<br />
<ul>

<strong>Webservers: </strong> <br /> <br />
Enabling SHA2 in Webservers is usually a matter of tweaking configuration. Providing the option to tweak VPN settings should contain an option to change the cipher suite or more specifically the hash algorithm. These are the list of Servers that support and do not support SHA2.<br /><br />

<strong>Servers – support SHA-256</strong><br />
Apache server and OpenSSL 0.9.8o+<br />
Apache 2.0.63+ , OpenSSL 1.1.x<br />
OpenSSL based servers - OpenSSL 0.9.8o+<br />
Windows Server 2003+ with patch 938397<br />
Windows Server 2003+ or XP client with patch 968730<br />
Windows Server 2008+<br />
Java based servers - 1.4.2+<br />
Cisco ACE module software version A4(1.0)<br />
Citrix Receiver models:<br />
  <ul>
  <li>Mac 11.8.2</li>
  <li>Windows 4.1 (std)</li>
  <li>Windows 3.4 (ent)</li>
  <li>Windows 8/RT (1.4)</li>
  </ul>
Oracle WebLogic v10.3.1+ see bug8422724<br />
Oracle Wallet Manager 11.2.0.3+<br />
IBM HTTP Server 8.5 (with Lotus Domino  9+)<br />
Juniper Secure Access -  SA 6.4R5, 6.5R3, and 7.0R1 and later releases.<br />
Websphere application Server v8.0.0.4<br /><br />

<strong>Servers which reportedly DO NOT support SHA-256 in their entirety</strong><br />

Juniper SBR<br />
IBM Domino<br />
<a href="https://www.citrix.com/content/dam/citrix/en_us/documents/data-sheet/citrix-workspace-app-feature-matrix.pdf?accessmode=direct">Citrix Receiver models</a><br />
Linux 13.0<br />
IOS 5.8.3<br />
Android 3.4.13<br />
Playbook 1.0<br />
Blackberry 2.2 / BlackBerry 1.0 Tech Preview<br />
Cisco ACE module software versions A2 and A3<br />
<br />
<li>
<strong>Apache: </strong> <br/>
To add SHA2 you just need to make sure that your SSLCipherSuite has the following cipher in your ‘https virtual host’ configuration:
<pre>
<code>
# Many ciphers defined here require a modern version (1.0.1+) of OpenSSL. Some
# require OpenSSL 1.1.0, which as of this writing was in pre-release.
SSLCipherSuite      ECDHE-ECDSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-GCM-SHA384:ECDHE-ECDSA-CHACHA20-POLY1305:ECDHE-RSA-CHACHA20-POLY1305:ECDHE-ECDSA-AES128-GCM-SHA256:ECDHE-RSA-AES128-GCM-SHA256:ECDHE-ECDSA-AES256-SHA384:ECDHE-RSA-AES256-SHA384:ECDHE-ECDSA-AES128-SHA256:ECDHE-RSA-AES128-SHA256
</code>
</pre>
You may realize that there are other cipher suites that have nothing to do with SHA2. The reason why the list has been provided is to ease cross checks or fresh configuration with the most secure protocols.<br /><br />

A good read: <a href="https://wiki.mozilla.org/Security/Server_Side_TLS"> Server Side TLS </a><br /><br />

<strong>Explanation: </strong><br />
<strong>Guide to reading cipher from configuration files: </strong><br /> <br />
One of the most popular formats look like this: <br />

<pre>
<code>...
ECDHE-RSA-AES128-GCM-SHA256
...</code>
</pre>
<br />
The above example shows a cipher suite seperate by another one from the list with a ':'. The first cipher 'ECDHE-RSA' specifies ECDHE+RSA as the signature algorithm for TLS while the AESGCM specifies the encryption scheme with its mode of operation. SHA256 specifies the hashing standard. <br /> <br />
<br />

<li>
<strong> Nginx: </strong> <br />
By default, the configuration file is named nginx.conf and placed in the directory /usr/local/nginx/conf , /etc/nginx , or /usr/local/etc/nginx.
<pre>
<code>...
ssl_ciphers ECDHE-RSA-AES256-GCM-SHA512:DHE-RSA-AES256-GCM-SHA512:ECDHE-RSA-AES256-GCM-SHA384:DHE-RSA-AES256-GCM-SHA384:ECDHE-RSA-AES256-SHA384;
...</code>
</pre> <br />

Similar to the Apache config above, these cipher suites provide the best security for VPN. Do not forget to restart the services and before doing so, measure the possible consequences of downtime. <br />
<pre>
<code>
$sudo nginx -t
$sudo service nginx restart
</code>
</pre>
</li>
<li>
<strong>Tomcat </strong> <br />
The configuration file for Tomcat should be in <br />
TOMCAT_HOME/conf/server.xml
<br /> <br />

Tomcat 5 & 6 (Prior to 6.0.38)
Within the server.xml find the sslProtocols entry and make sure only secure cipher suites (with SHA2 as minimum security)  are specified: <br />

An example of server.xml is: <br />

<code>
<pre>Example SSL Connector: (Tomcat 7 w/Java 7)
&ltConnector port="443" maxHttpHeaderSize="8192" address="192.168.1.1"
enableLookups="false" disableUploadTimeout="true"
acceptCount="100" scheme="https" secure="true" clientAuth="false"
keystoreFile="SomeDir/SomeFile.key" keystorePass="Poodle"
truststoreFile="SomeDir/SomeFile.truststore" truststorePass="HomeRun"
sslProtocol="TLSv1, TLSv1.1, TLSv1.2"
ciphers="TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384,
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384,
TLS_ECDH_ECDSA_WITH_AES_256_CBC_SHA384,
TLS_ECDH_RSA_WITH_AES_256_CBC_SHA384,
TLS_DHE_DSS_WITH_AES_256_CBC_SHA256,
TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA,
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA,
TLS_ECDH_ECDSA_WITH_AES_256_CBC_SHA,
TLS_ECDH_RSA_WITH_AES_256_CBC_SHA,
TLS_DHE_DSS_WITH_AES_256_CBC_SHA,
TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256,
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256,
TLS_ECDH_ECDSA_WITH_AES_128_CBC_SHA256,
TLS_ECDH_RSA_WITH_AES_128_CBC_SHA256,
TLS_DHE_DSS_WITH_AES_128_CBC_SHA256,
TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA,
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA,
TLS_ECDH_ECDSA_WITH_AES_128_CBC_SHA,
TLS_ECDH_RSA_WITH_AES_128_CBC_SHA,
TLS_DHE_DSS_WITH_AES_128_CBC_SHA,
TLS_ECDHE_ECDSA_WITH_RC4_128_SHA,
TLS_ECDH_ECDSA_WITH_RC4_128_SHA,
TLS_ECDH_RSA_WITH_RC4_128_SHA,
TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384,
TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256,
TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384,
TLS_RSA_WITH_AES_256_GCM_SHA384,
TLS_ECDH_ECDSA_WITH_AES_256_GCM_SHA384,
TLS_ECDH_RSA_WITH_AES_256_GCM_SHA384,
TLS_DHE_DSS_WITH_AES_256_GCM_SHA384,
TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256,
TLS_RSA_WITH_AES_128_GCM_SHA256,
TLS_ECDH_ECDSA_WITH_AES_128_GCM_SHA256,
TLS_ECDH_RSA_WITH_AES_128_GCM_SHA256,
TLS_DHE_DSS_WITH_AES_128_GCM_SHA256,
TLS_ECDHE_ECDSA_WITH_3DES_EDE_CBC_SHA,
TLS_ECDHE_RSA_WITH_3DES_EDE_CBC_SHA,
TLS_ECDH_ECDSA_WITH_3DES_EDE_CBC_SHA,
TLS_ECDH_RSA_WITH_3DES_EDE_CBC_SHA,
TLS_EMPTY_RENEGOTIATION_INFO_SCSVF
"/&gt </pre></code>

Restart the Tomcat service to complete the changes. <br /> <br /> <br /> <br />

<strong>Browsers: </strong> <br /> <br />

It is important the client side is also protected against attacks where weak ciphers are negotiated with servers that you might not control. To ensure that the clients are protected, browsers should support SHA2. Almost every browser (if not all) support SHA2 as it has been around for a long time.
<br />
These are the browsers that current support SHA2:  <br /> <br />

Adobe Acrobat/Reader 7<br />
Blackberry 5+ <br />
Chrome 26+ <br />
Chrome under Linux <br />
Chrome under Mac from Mac OS X 10.5 <br />
Chrome under Windows Vista and higher <br />
Firefox 1.5+ <br />
Internet Explorer 7+ and higher <br />
Internet Explorer 7+ under Vista <br />
Internet Explorer 6+ under Windows XP SP3 (patched) <br />
Java 1.4.2+ based products <br />
Konqueror 3.5.6+ <br />
Mozilla 1.4+ <br />
Mozilla products based on NSS 3.8+ (since April 2003)<br />
Netscape 7.1+ <br />
Opera 9.0+ <br />
Products based on OpenSSL 0.9.8o+ <br />
Safari from Mac OS X 10.5+ <br />
Windows Phone 7+ <br />

	<h2> <img src="/img/common/patch.png " style="width:100px;height:100px;" /> Upgrade/Patch Management </h2>
	<font size="4"><strong>Concept:</strong></font> There are no notable patches or upgrades that are present for any of the popular products using SHA2. But IT administrators should always keep a close watch on any patches or upgrade notifications from product vendors. The expectation is that these patches will not particularly target protocol vulnerabilities but rather implementation ones. For example, a software bug in Cisco product allows compromise of SHA2's security. Understanding a newly released patch or upgrade should be possible by reading its respective documentation and queries of any sort should be clarified with the product manufacturers to ensure a smooth process with no adverse impacts.
<br /> <br /> <strong> Note: </strong>
Keep an eye out for this section as it will be kept up-to-date with any major patches that are released.
</p>
