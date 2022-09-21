---
layout: quickstart
title: "IT Admin's QuickStart"
type: TLS 1.3
qtype: it
upper-link: /articles/cryptographic_protocols/tls_1_3/tls_1_3.html
image: /img/common/NewDevLogo.png
note: "An introduction to where TLS is leveraged in an IT ecosystem, including where configuration files and pertinent security controls live on a system."
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
    link: https://docs.python.org/2/library/ssl.html
---
<p id="GeneralTLSInfo">

<h2> <img src="/img/common/configuration.jpg" style="width:110px;height:100px;" /> TLS 1.3 Configuration </h2>

 <div class="timestamp">
    <p><span>Last Updated Sun, 15 Apr 2018 2:02:01 -0400</span></p>
  </div>

<font size="4"><strong>What to expect:</strong></font><br /> <br />

<font size="4"><strong>Concept:</strong></font> TLSv1.3 is new. As discussed on the <a href="/articles/cryptographic_protocols/tls_1_3/tls_1_3.html">landing page </a>, vulnerable security measures have been removed from the protocol. There are no known vulnerabilities that exists with the current version. We however recommend that you go through the following page in order to understand why and when to upgrade?
<br /> <br />

<font size="3"><strong>Examples for Enabling TLSv1.3:</strong></font> <br />
<br />We have categorized the examples into three sections:- Webservers and Browsers. <br />
<br />
<ul>

<strong>Webservers: </strong> <br /> <br />
TLS 1.3 is supported starting from Nginx 1.13 version. If you are running older version then first you got to upgrade.
<br /><br />

<strong> Nginx: </strong> <br />
<ul>
<li>Login to Nginx server</li>
<li>Take a backup of nginx.conf file</li>
<li>Modify nginx.conf using vi or your favorite editor</li>
</ul>

<br />
The default configuration under SSL settings should look like this:
<pre>
<code>...
ssl_protocols TLSv1.2;
...</code>
</pre> <br /> <br />

Add TLSv1.3 at the end of the line, and so it looks like below:
<pre>
<code>...
ssl_protocols TLSv1.2 TLSv1.3;
...</code>
</pre>

Similar to the Apache config above, you will get TLSv1.0+ support and no SSL. You can check the config and restart.
<pre>
<code>
$sudo nginx -t
$sudo service nginx restart
</code>
</pre>

<strong>Browsers: </strong> <br /> <br />

<ul>
<li>
<strong>Firefox Nightly</strong> <br />
<ul>
<li>Install and run Firefox nightly: <a href="https://nightly.mozilla.org/">https://nightly.mozilla.org/</a></li>
<li>Enter "about:config" in the address bar</li>
<li>Set security.tls.version.max from 3 to 4</li>
<li>Restart the browser</li>
</ul>
</li> <br />

<li>
<strong>Chrome Canary</strong> <br />
<ul>
<li>Install and run Chrome Canary: <a href="https://www.google.com/chrome/browser/canary.html">https://www.google.com/chrome/browser/canary.html</a></li>
<li>Enter "chrome://flags/" in the address bar </li>
<li>Go to "Maximum TLS version enabled." and select "TLS 1.3" </li>
<li>Restart the browser </li>
</ul>
</li> <br /> <br />

In order to test if a domain is TLSv1.3 compatible: <a href=" https://www.ssllabs.com/ssltest/">https://www.ssllabs.com/ssltest/</a>

<br />


<h2> <img src="/img/common/patch.png" style="width:100px;height:100px;" /> Upgrade/Patch Management </h2>

<font size="4"><strong>Concept:</strong></font> TLSv1.3 is a relatively new protocol. A lot of products are still in the process of supporting it. The only major decision at this point of time would be to use TLSv1.3 or not rather than what are the upgrades to TLSv1.3. But, since the protocol is still in draft, expect changes and therefore expect upgrades/patches. As always, we recommend that you read through the product specific advisories
before taking any decision.

<br /> <br /> <strong> Note: </strong>
Keep an eye out for this section as it will be kept up-to-date with any major patches that are released.

<br /> <br />
Some examples of advisories that you can find: <br />
<a href="https://forum.nginx.org/read.php?27,273840,273840#msg-273840">https://forum.nginx.org/read.php?27,273840,273840#msg-273840</a> <br />
<a href="https://community.akamai.com/community/web-performance/blog/2017/10/25/get-ready-for-tls-13">https://community.akamai.com/community/web-performance/blog/2017/10/25/get-ready-for-tls-13</a>
