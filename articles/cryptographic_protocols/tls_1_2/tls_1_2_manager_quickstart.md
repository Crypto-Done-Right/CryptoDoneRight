---
layout: quickstart
title: "Manager's QuickStart"
type: TLS 1.2
qtype: manager
upper-link: /articles/cryptographic_protocols/tls_1_2/tls_1_2.html
image: /img/common/NewDevLogo.png
note: "Are you a Manager? Get started with best practice setup details above."
col: col-md-8 col-sm-8 col-xs-8 infoBlocks
alerts:
  - id: 1
    type: danger
    description: There are serious security implications if not configured properly!
    link: ""
further-reading:
  - name: "RFC 5246: The Transport Layer Security (TLS) Protocol Version 1.2"
    link: https://tools.ietf.org/html/rfc5246
  - name: "RFC for secure use of SSL, TLS and DTLS"
    link: https://datatracker.ietf.org/doc/rfc7525/?include_text=1
related-articles:
  - name: "Book: Understanding SSL, TLS and PKI"
    link: tps://www.feistyduck.com/books/bulletproof-ssl-and-tls
---
<p>
  <h3>Management QuickStart</h3>
  SSL/TLS is one of the most popular technology that aims at, mainly through cryptography, securing communication between different networks. SSL provides a way for two parties to establish a session and transfer data over the session while ensuring privacy, confidentiality and integrity. All secure communications on the internet at this moment use this same technology (HTTPS). Some of the popular software applications that use SSL are VPNs and Web Browsers. For example, in client-server environment, an SSL link ensures that all data passed between the web server and browsers remain private and integral. SSLv2 and TLSv1 are the 2 versions of this protocol (SSLv1 was never publicly released). After TLSv1, SSL was renamed to TLS. Those protocols are standardized and described by RFCs.
  <br /> <br />

<h4><img src="/img/common/protocol.png" style="width:80px;height:80px;"/>Protocol:</h4>
  TLSv1 is not safe. It has a few critical vulnerabilities and is rightly being decommissioned by a lot of popular vendors and product manufacturers. There have been major flaws found with TLSV1 protocol such as <a href="https://blog.qualys.com/ssllabs/2013/09/10/is-beast-still-a-threat">Beast</a>. There were other factors too apart from the vulnerabilities that led to TLSv1 being marked as an obsolete technology. Since this is a flaw in the official definition and standardization of the protocol, the only option to fix this issue is to upgrade the version of SSL (now being called TLS) being used. Note that upgrading the protocol does not result in any difference in what SSL was intended to do (secure communication), an upgrade to the protocol simply means that the technology is patched for flaws that could compromise the security of the product using it.
  <br /> <br />
  <h5>High-level Action Plan: </h5>
  <ul>
  <li> Disable TLSv1 on all systems. Should be used in no capability whatsoever.</li> <br />
  <li> Upgrade to TLSv1.2 is recommended. TLSv1.1 can also be considered for a temporary basis. Have the appropriate teams (Ex: IT and Development) clearly informed and prepared for an upgrade.</li> <br />
  <li> Connectivity to these systems using TLSv1 could be affected because of the upgrade. Ensure proper migration plan to avoid implications like unnecessary downtime.</li> <br />
  <li> Run an audit to make sure that the upgrade was successful.</li> <br />
  <li> In any case if an upgrade is not possible, it is recommended in the interest of security to turn off all SSL connectivity to the system (Ex: remote access VPNs, web page hosting over HTTPS).</li> <br />
  <br /> <br />
  </ul>

<h4><img src="/img/common/implementation.png " style="width:100px;height:100px;"/>Implementation:</h4>

  Note: Only think about Implementation if you are in a situation where legacy hardware or software cannot be upgraded to support at least TLSv1.1
  <br /> <br />
  A lot of vendors who support TLSv1 should provide software patches that should help prevent protocol vulnerabilities. If any of these patches are present and can be implemented on a system that runs TLSv1, they should be done immediately. This would require extensive research of specific products and therefore there is no documentation on this site (except examples under IT or Dev Quickstart). General practices for good patch management should be followed. For example, the patches should be verified for genuineness and the patch should specifically solve problems with TLSv1. It should also be noted that patches will only work if both sides of a connection (client and server) have been patched.
   <br /> <br />
  <h5>High-level Action Plan: </h5>
  <ul>
  <li> List down hardware or software that cannot be upgraded. </li> <br />
  <li> Gather the respective teams responsible for administration and management of these devices or technology. </li> <br />
  <li> Teams should be tasked with finding the patches and devising a plan to implement them ASAP. </li> <br />
  <li> Consider any sort of verification process to audit these patches. </li> <br />
  <li> Devise a long term plan to replace the hardware or software to support TLSv1.1 at the least. </li> <br />
  <br /> <br />
  </ul>

<h4><img src="/img/common/configuration.jpg " style="width:110px;height:100px;" />Configuration:</h4>

  TLSv1.2 offer a few options with configuration. Some of these are Cipher Suites, Key lengths, Hash Functions used by your CA to sign your keys. Keep in mind that the security of your system is only as strong as the weakest link in the chain. For example, a strong cipher alone does not guarantee good security. The keys and the certificates are just as important, as well as the hash functions and keys used by the Certification Authority (CA) to sign your keys. The parameters for these settings depend on the version of SSL/TLS that is being used and therefore great care must be taken in choosing the best combination of the above settings.
  <br /> <br />
  <h5>High-level Action Plan: </h5>
  <ul>
  <li> Gather teams that are responsible for configuring TLSv1.2. Teams who take care of Cipher Suits, Key lengths, Hash Functions used by your CA to sign your keys, are very important.</li> <br />
  <li> Have team research the best set of parameters to be configured to provide maximum security with TLSv1.2. These details can be found on this site under IT and Dev Quickstarts.</li> <br />
  <li> Keep in mind interoperability with different devices that support TLSv1. The configurational changes should match on both the ends of any TLSv1.2 connections.</li> <br />
  <li> Changes in configuration can be done on the fly on a lot of products. Take steps to ensure unnecessary downtime.</li> <br />
  <li> If there are no changes possible on any devices, there are no alternatives to fixing security problems with TLSv1.</li> <br />
