---
layout: quickstart
title: IT Admin's QuickStart
type: SHA1
qtype: it
upper-link: /articles/hashing_algorithms/sha1.html
image: /img/common/manager.png
note: "Are you a Manager? Get started with best practice setup details above."
col: col-md-4 col-sm-4 col-xs-4 infoBlocks
---
 <p id="when">
            <strong>When is SHA used?</strong>
            SHA is primarily being used for the following purposes:
            <ol><li>
                Cryptography:- SHA-1 forms part of several widely used security applications and protocols, including TLS and SSL, PGP, SSH, S/MIME, and IPsec.
              </li>
              <li>
                Data Integrity:- This means a hash or SHA-1 helps to identify revisions, and to detect data corruption or tampering. In other words, it is a consistency check. It ensures if some data is, if checked at a later time or after transit, then the received data is consistent and not tampered with.
              </li>
              <li>
                Password Storage:- Described in the above example
              </li>
            </ol>
          </p>

<p id="identification">
            <strong>How do I know if I am using SHA-1 in my IT systems or infrastructure?</strong><br /> <br />
            As described in the migration page, it is essential to gather and create a comprehensive list or an inventory of every unique devices, OS or application in your infrastructure.
            <ol><li>
                Identify the systems that use certificates.If certificates are in use, you must check if SHA-1 signature is in use for those certificates or not. You can check by visiting the site in your browser and viewing the certificate that the browser received. The details of how to do that can vary from browser to browser, but generally if you click or right-click on the lock icon, there should be an option to view the certificate details. In the list of certificate fields, look for one called "Certificate Signature Algorithm". (For StackOverflow's certificate, its value is "PKCS #1 SHA-1 With RSA Encryption".)
              </li>
              <li>
                If your infrastructure has a web server, you can use the following site and see if you are using the SHA-1 or some other certificate. The site is <a href="https://shachecker.com/">https://shachecker.com/</a> or <a href="https://shaaaaaaaaaaaaa.com/">https://shaaaaaaaaaaaaa.com/</a>.
              </li>
              <li>
                Here, is a quick command in a linux system that you can run to know if you are using the correct SHA-1 certificate.<br><br>
                <pre>
<code>$openssl s_client -connect www.yoursite.com:443 < /dev/null 2>/dev/null \ | openssl x509 -text -in /dev/stdin | grep "Signature Algorithm"</code></pre>
<strong>OR</strong><br>
<pre><code>$openssl s_client -connect \<host\>:\<port\> < /dev/null 2>/dev/null | openssl x509 -text -in /dev/stdin | grep "Signature Algorithm"</code></pre>
          <p>
            One real-world example where SHA-1 may be used is when you're entering your password into a website's login page. Though it happens in the background without your knowledge, it may be the method a website uses to securely verify that your password is authentic.
          </p>
          <p>
            In this example, imagine you're trying to login to a website you often visit. Each time you request to log on, you're required to enter in your username and password.
          </p>
          <p>
            If the website uses the SHA-1 cryptographic hash function, it means your password is turned into a checksum after you enter it in. That checksum is then compared with the checksum that's stored on the website. If the two match, you're granted access; if they don't, you're told the password is incorrect.
          </p>
          <p>
            Another example where the SHA-1 hash function may be used is for file verification. Some websites will provide the SHA-1 checksum of the file on the download page so that when you download the file, you can check the checksum for yourself to ensure that the downloaded file is the same as the one you intended to downloaded.
          </p>

<p id="where">
            <strong>Protocols Used In:</strong>
            <ul>
              <li>Transport Layer Security (TLS)</li>
              <li>Secure Sockets Layer (SSL)</li>
              <li>Pretty Good Privacy (PGP)</li>
              <li>Secure Shell (SSH)</li>
              <li>Secure/Multipurpose Internet Mail Extensions (S/MIME)</li>
              <li>Internet Protocol Security (IPSec)</li>
            </ul>
          </p>
          <p id="whenToUse">
            <strong>When and Where is SHA-1 Ok?</strong>
            Checking the hash of an executable or file that we know is trusted (from trusted site).
            No known flaws in SHA-1 as a key derivation function which is how dh-group14-sha1 is being used.  
            Similarly, HMAC-SHA1 is believed to be (still) safe as long as SHA1 is pseudorandom.   
            The specific construct of HMAC-SHA1 is still considered safe to use (assuming a secret key) due to the security proof for HMAC which does not rely on collision resistance of the underlying PRF.
          </p>

<br /> <br />

<h3>Web Administrator's Configuration Guide - Microsoft Servers</h3>
<br /> <br />
<p>
            As per Microsoft's SHA-1 deprecation policy, Windows users don't need to do anything in response to this new technical requirement. XP Service Pack 3 (SP3) and later versions support SHA-2 SSL certificates. Server 2003 SP2 and later versions add SHA-2 functionality to SSL certificates by applying hotfixes (KB968730 and KB938397).
          </p>
          <p>
            <span class="green">Web administrators must request new certificates to replace SHA-1 SSL and code-signing certificates that expire after January 1, 2017.</span> As of this writing, that would probably affect only public SHA-1 certificates that were purchased with a long expiration date (three years or more) or long-duration certificates issued by internal SHA-1 CAs. Most third-party CAs will rekey their certificates for free, so you simply need to contact the CA to request a rekeyed certificate that uses the SHA-2 algorithm.
          </p>
          <p>
            When ordering new SSL certificates, you should confirm with the CA that they're being issued with the SHA-2 algorithm. New certificates with expiration dates after January 1, 2017, can only use SHA-2. Code-signing certificates with expiration dates after December 31, 2015, must also use SHA-2.
          </p>
          <p>
            Note that the algorithm used in SHA-2 certificates is actually encoded to use SHA-256, SHA-384, or SHA-512. All of these are SHA-2 algorithms; the SHA number (e.g., 256) specifies the number of bits in the hash. The larger the hash, the more secure the certificate but possibly with less compatibility.
          </p>
          <p>
            <span class="green">It's important that the certificate chain be encrypted with SHA-2 certificates. (A certificate chain consists of all the certificates needed to certify the end certificate.)</span> This means that any intermediate certificates must also use SHA-2 after January 1, 2017. Typically, your CA will provide the intermediate and root CA certificates when they provide the SHA-2 certificate. Sometimes they provide a link for you to download the certificate chain. It's important that you update this chain with SHA-2 certificates. Otherwise, Windows might not trust your new SHA-2 certificate.
          </p>
          <p>
            Root certificates are a different story. These can actually be SHA-1 certificates because Windows implicitly trusts these certificates since the OS trusts the root certificate public key directly. A root certificate is self-signed and isn't signed by another entity that has been given authority.
          </p>
          <p>
            For the same reason, any self-signed certificate can use the SHA-1 algorithm. For example, Microsoft Exchange Server generates self-signed SHA-1 certificates during installation. These certificates are exempt from the new SHA-2 policy since they aren't chained to a CA. I expect, however, that future releases of Exchange will use SHA-2 in self-signed certificates.
          </p>

<br />
          <h3 id="enterprise">What About My Enterprise CAs</h3>
          <p>
            If your organization has its own internal CA PKI, you'll want to ensure that it's generating SHA-2 certificates. How this is done depends on whether the CA is running Windows Server 2008 R2 or later and if your CA has subordinate CAs.
          </p>
          <p>
            If you have a Server 2008 R2 or later single-root CA without subordinates, you should update the CA to use SHA-2. Doing so will ensure that subsequent certificates generated will use the SHA-2 algorithm. To check which hash algorithm is being used, you can right-click the CA and go to the General tab. If SHA-1 is listed, you can run the following certutil command to configure the CA to use the SHA-256 algorithm:
            <xmp>
            certutil -setreg ca\csp\CNGHashAlgorithm SHA256
            </xmp>
          </p>
          <p>
            You must restart the CertSvc service to apply the change. Now when you view the CA properties, you'll see that the hash algorithm is SHA-256. All future certificates issued by this CA will use SHA-256, but keep in mind that existing certificates will still be using SHA-1. You need to renew any SHA-1 certificates issued by this CA to upgrade them to SHA-2 certificates.
          </p>
          <p>
            <span class="red">If your CA is older than Server 2008 R2, you can't upgrade the CA to use SHA-2. You'll need to rebuild it with a newer version.</span> If your organization's internal CA is multi-tiered with one or more subordinate CAs, you'll need to reconfigure them to use SHA-2. This is done using the same certutil command just given on each subordinate or issuing CA. Keep in mind that if you use subordinate CAs, you're not required to update the root CA to SHA-2 since that certificate is at the top of the certificate chain, but it won't cause any problems if you do. You still need to renew any SHA-1 certificates issued by the subordinate CAs to upgrade them to SHA-2 certificates.
          </p>

<br />
          <h3 id="action">Take Action Now</h3>
          <p>
            Administrators and website operators should identify all the SSL certificates used in their organizations and take action, as follows:
            <ul>
              <li>
                SHA-1 SSL certificates expiring before January 1, 2017, will need to be replaced with a SHA-2 equivalent certificate.
              </li>
              <li>
                SHA-1 SSL certificates expiring after January 1, 2017, should be replaced with a SHA-2 certificate at the earliest convenience.
              </li>
              <li>
                Any SHA-2 certificate chained to an SHA-1 intermediate certificate should be replaced with another one chained to an SHA-2 intermediate certificate.
              </li>
            </ul>
          </p>
