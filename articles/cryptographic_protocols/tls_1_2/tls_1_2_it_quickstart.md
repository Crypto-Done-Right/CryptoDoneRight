---
layout: quickstart
title: "IT Admin's QuickStart"
type: TLS 1.2
qtype: it
upper-link: /articles/cryptographic_protocols/tls_1_2/tls_1_2.html
image: /img/common/NewDevLogo.png
note: "Are you an IT administrator? Get started with best practice setup details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
further-reading:
  - name: "TLSv1.2 RFC"
    link: https://tools.ietf.org/html/rfc5246
  - name: "Hardening TLS on RedHat Servers"
    link: https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/sec-hardening_tls_configuration
related-articles:
  - name: "List of all changes between TLSv1.1 and 1.2"
    link: https://www.wolfssl.com/a-comparison-of-differences-in-tls-1-1-and-tls-1-2/
  - name: "Enabling TLSv1.2 on Microsoft machines"
    link: https://support.microsoft.com/en-us/help/3140245/update-to-enable-tls-1-1-and-tls-1-2-as-a-default-secure-protocols-in
  - name: "Hynek Schlawack: Hardening Your Web Server's SSL Ciphers"
    link: https://hynek.me/articles/hardening-your-web-servers-ssl-ciphers
---
<p id="GeneralTLSInfo">

<h2> <img src="/img/common/configuration.jpg " style="width:110px;height:100px;" /> TLS 1.2 Configuration </h2>

<font size="4"><strong>What to expect:</strong></font><br /> <br />
For TLSv1.2, the following configuration settings will provide the best possible security (mitigation of all known vulnerabilties):
<ul>
<li>Enabling TLSv1.2 - First step is to ensure that your devices are configured for accepting and establishing TLSv1.2 connections. For security reason, it also needs to be further ensured that older versions of SSL/TLS are disabled. Server and Client must reject any connections offering SSL 1.0, SSL 2.0, SSL 3.0, TLS 1.0, TLS 1.1
</li>
<li>Cipher Suites: A configurable option that most product vendors provide with SSL/TLS is called the Cipher Suite. The cipher suite decides the key exchange, signature, encryption and hashing algorithm used with SSL/TLS. There are various options with all the above mentioned parameters and some of them have been marked as unsafe due to vulnerabilities found in recent times. Special care must be taken to ensure that TLSv1.2 is configured correctly and below are the recommended cipher suites. The recommendations are based on a recent attack called a ROBOT attacks <a href="tls-1-2-vuln.html">Learn more</a>.</li>
<li>DH Parameters: Diffie Helman Key Exchange protocol is a popular protocol option for exchanging keys between a server and a client in a secure fashion. SSL/TLS provides options to use DH but it should be ensured that the right kind of keys are configured for the protocol. The recommendations are based on the LogJam attack<a href="tls-1-2-vuln.html#logjam">Learn more</a>.</li>
<li>Type of Certificates: Certificates form the basis of authentication in SSL/TLS. Using certificates the client can authenticate the server and vice versa (although client side authentication using certificates is optional). </li>
<li>Key type and Size: Apart from DH keys, there are other keys that are used for digital signature purposes. Choosing the right kind of keys is important.
</li> <br />
For the above settings, there have been examples mentioned below.
</ul> <br />
<font size="4"><strong>Concept:</strong></font> TLSv1.2 as a protocol is, as of now, safe. But, if configured incorrectly, your device can still be vulnerable. In this section, using a certain few examples
explore how configuration is setup to enable TLSv1.2 with right settings. Since there are no vulnerabilities that have been found with this version <strong>yet</strong>, we cover as to how you can check if your connections are TLSv1.2. Again, note that enforcement of TLSv1.2 on all connections is <span class="green">recommended</span> for security.
<br /> <br />

<span class="red">Note: Enabling TLSv1.2 on your device is the first step that is to be taken towards ensuring security. However, recent vulnerabilities discovered in certain options provided by the
protocol mandate that the configuration of TLSv1.2 also follows certain guidelines.These recommendations have been mentioned in the later part of this section under <a href="#GeneralTLSInfoDebra">General Recommendations of TLS </a>.
</span>

<br /> <br />
<font size="3"><strong>Examples for Enabling TLSv1.2:</strong></font> <br />
<br />We have categorized the examples into three sections:- Webservers, Browsers and VPN. <br />
<br />
<ul>

<strong>Webservers: </strong> <br /> <br />
Enabling TLSv1.2 under the web server’s SSL configuration settings is required. It is required to leave out vulnerable versions of SSL from the configuration so that legacy clients are not able to connect until an upgrade is performed. Here are a couple of examples from common webservers on how this can be done.
<br /><br />
<strong>Apache: </strong> <br/>
To add TLSs1.2 you just need to add in your ‘https virtual host’ configuration:
<pre>
<code>...
SSLProtocol -all +TLSv1.2
...</code>
</pre>

Explanation: <br />
-all is removing other ssl protocol (SSL 1,2,3 TLS1)<br />
+TLSv1.2 is adding TLS 1.2<br /> <br />

For more browser compatibility you can use:- <br />
<pre>
<code>...
SSLProtocol -all +TLSv1.2
...</code>
</pre>

<strong> Nginx: </strong> <br />
By default, the configuration file is named nginx.conf and placed in the directory /usr/local/nginx/conf , /etc/nginx , or /usr/local/etc/nginx.
<pre>
<code>...
ssl_protocols TLSv1.2;
...</code>
</pre> <br /> <br />

Similar to the Apache config above, you will get TLSv1.0+ support and no SSL. You can check the config and restart.
<pre>
<code>
$sudo nginx -t
$sudo service nginx restart
</code>
</pre>

To enforce TLSv1.2:

<pre>
<code>...
ssl_protocols TLSv1.2
...</code>
</pre>

<strong>Tomcat </strong> <br />
The configuration file for Tomcat should be in <br />
TOMCAT_HOME/conf/server.xml
<br /> <br />

Tomcat 5 & 6 (Prior to 6.0.38 <br /> <br />
Within the server.xml find the sslProtocols entry and make sure only TLS protocols are specified: <br />

<pre>
<code>sslProtocols = "TLSv1.2"</code>
</pre>

Tomcat 6 & 7 (6.0.3.8 and newer) <br /> <br />
Within the server.xml file, find the sslEnabledProtocols entry and make sure only TLS protocols are specified: <br />
<pre>
<code>sslEnabledProtocols = "TLSv1.2"</code>
</pre>

Restart the Tomcat service to complete the changes. <br /> <br /> <br /> <br />

<strong>Browsers: </strong> <br /> <br />

Technically the attack is a client based and although ensuring servers do not accept SSLv3 connections, it is important to plug the problem on the client side as well.
Here are some common browsers where configuration changes can be made so as to make sure that only connections on TLSv1.2 are accepted.
<br />
To enable TLS 1.2 protocols on web browsers, see the list below. <br /> <br />
<ul>

<li>
<strong>Microsoft Internet Explorer</strong> <br />
<ul>
<li>Open Internet Explorer</li>
<li>From the menu bar, click Tools >  Internet Options > Advanced tab</li>
<li>Scroll down to Security category, manually check the option box for Use TLS 1.2 </li>
<li>Click OK</li>
<li>Close your browser and restart Internet Explorer</li>
</ul>
</li> <br />

<li>
<strong>Google Chrome</strong> <br />
<ul>
<li>Open Google Chrome </li>
<li>Click Alt F and select Settings </li>
<li>Scroll down and select Show advanced settings... </li>
<li>Scroll down to the Network section and click on Change proxy settings... </li>
<li>Select the Advanced tab </li>
<li>Scroll down to Security category, manually check the option box for Use TLS 1.2 </li>
<li>Click OK </li>
<li>Close your browser and restart Google Chrome </li>
</ul>
</li> <br />

<li>
<strong>Mozilla Firefox </strong> <br />
<ul>
<li>Open Firefox</li>
<li>In the address bar, type about:config and press Enter </li>
<li>In the Search field, enter tls. Find and double-click the entry for security.tls.version.min</li>
<li>Set the integer value to 3 to force protocol of TLS 1.2 </li>
<li>Click OK</li>
<li>Close your browser and restart Mozilla Firefox</li>
</ul>
</li> <br />

<li>
<strong>Opera </strong> <br />
<ul>
<li>Open Opera</li>
<li>Click Ctrl plus F12</li>
<li>Scroll down to the Network section and click on Change proxy settings...</li>
<li>Select the Advanced tab</li>
<li>Scroll down to Security category, manually check the option box Use TLS 1.2</li>
<li>Click OK</li>
<li>Close and restart Opera</li>
</ul>
</li> <br />

<li>
<strong>Apple Safari </strong> <br />
There are no options for enabling SSL protocols. If you are using Safari version 7 or greater, TLS 1.1 and TLS 1.2 are automatically enabled.
</li> <br />

</ul>

<strong>VPN: </strong> <br />
The VPN gateway needs to be configured to only accept TLSv1.2 connection. Apart from configuration, patches provided by the software company should be installed with immediate priority.
<br /> <br />
To verify:
<a href="https://www.ssllabs.com/ssltest/index.html">https://www.ssllabs.com/ssltest/index.html</a>
</ul>

<span class="red"> Note: Configuring TLSv1.2 - After ensuring that your device is ready to accept TLSv1.2 connections. The next step is to ensure that TLSv1.2 connections are hardened in order to provide best security. A common misconception is why are we "reconfiguring" TLSv1.2 while it's already setup. It has to be noted that the first step was only to setup TLSv1.2, the first step is to ensure that your devices are configured to accept and establish TLSv1.2 connections. For security reasons, it also needs to be ensured that the encryption, key exchange and hashing methods are tweaked for maintaining confidentiality and integrity. </span> <br /><br />

<strong>Guide to reading cipher from configuration files: </strong><br /> <br />
One of the most popular formats look like this: <br />

<pre>
<code>...
ECDH+AESGCM:ECDH+AES256
...</code>
</pre>
<br />
The above example shows two cipher suites separated by a ':'. The first cipher 'ECDH+AESGCM' specifies ECDH as the signature algorithm for TLS while the AESGCM specifies the encryption scheme with its mode of operation. The second cipher, ECDH:AES256 specifies ECDH being used as the signature scheme and AES256 talks about the encryption algorithm. The mode of operation will be whatever is the system default. <br /> <br />


<p id="GeneralTLSInfoDebra">
<font size="3"><strong>Recommended Cipher Suites</strong></font> <br /> <br />

<strong>TLS Recommended Ciphers:</strong><br />
TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256 as defined in RFC 5289<br />
TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384 as defined in RFC 5289<br />
TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 as defined in RFC 5289<br />
TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 as defined in RFC 5289<br />
TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 as defined in RFC 5289<br />
TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 as defined in RFC 5289<br />
TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 as defined in RFC 5289<br />
TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 as defined in RFC 5289<br /><br />

<strong>Disable the following ciphers:</strong> <br />
TLS_DHE_RSA_WITH_AES_128_CBC_SHA <br />
TLS_DHE_RSA_WITH_AES_256_CBC_SHA <br />
TLS_DHE_RSA_WITH_AES_128_CBC_ SHA256 <br />
TLS_DHE_RSA_WITH_AES_256_CBC_ SHA256 <br />
TLS_RSA_WITH_AES_128_CBC_SHA <br />
TLS_RSA_WITH_AES_256_CBC_SHA <br />
TLS_RSA_WITH_AES_128_CBC_SHA256 <br />
TLS_RSA_WITH_AES_256_CBC_SHA256 <br /> <br />

The problem with this is that using RSA for key exchange does not provide perfect forward secrecy since you are not using ephemeral “one-time use” keys which means they are susceptible to the <a href="https://robotattack.org/">ROBOT Attack.</a> <br /> <br />

<strong>Note:</strong> <br />

<strong>More info on why not to use DHE and use ECDHE instead:</strong>
The DHE ciphers are safe to use only if dh group 14 (2048 bit) key sizes are being used for key exchange. If a lower dh group size is used with DHE ciphers then your server will be susceptible to the <a href="ssl-3-vuln.html">Logjam</a> attack  This setting may have to be set in the OpenSSL code. There is not a configurable option external to the openssl module. Apache allows for configuring the dh parameters via their management interface but extreme care should be taken in order to avoid unecessary implications by tweaking such settings. In order to keep things simple and safe, use ECDHE. There are other benefits which have been well described <a href="https://security.stackexchange.com/questions/14731/what-is-ecdhe-rsa">here</a>.
Here is another good write-up: <a href="http://crypto.stackexchange.com/questions/15329/tls-ssls-usage-of-non-ephemeral-dh-vs-dhe"> Usage of non-ephermeral-dh vs dhe </a>.<br /><br />
</p>

<h2> <img src="/img/common/patch.png " style="width:100px;height:100px;" /> Upgrade/Patch Management </h2>

<font size="4"><strong>Concept:</strong></font> There are no notable patches or upgrades that are present for any of the popular products using TLSv1.2. But IT administrators should always keep a close watch on any patches or upgrade notifications from product vendors. The expectation is that these patches will not particularly target protocol vulnerabilities but rather implementation ones. For example, a software bug in Cisco product allows compromise of TLSv1.2's security. Understanding a newly released patch or upgrade should be possible by reading its respective documentation and queries of any sort should be clarified with the product manufacturers to ensure a smooth process with no adverse impacts.
 <br /> <strong> Note: </strong>
Keep an eye out for this section as it will be kept up-to-date with any major patches that are released.

</p>
