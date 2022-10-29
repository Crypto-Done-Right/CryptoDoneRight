---
layout: quickstart
title: Guide
permalink: /flaw_categories.html
further-reading:
  - name: DROWN attack
    link: "https://blog.cryptographyengineering.com/2016/03/01/attack-of-week-drown/"
  - name: RFC with all attacks against TLS and DTLS
    link: "https://tools.ietf.org/html/rfc7457"

related-articles:
  - name: Bruce Schneier:Another New AES Attack
    link: "https://www.schneier.com/blog/archives/2009/07/another_new_aes.html#"

---
<p>
  <div style="margin-top:2vw;">
    <h3>Generic Steps for Understanding Flaws</h3>
  </div>

  There are three major categories that one would need to consider while deciding a standard or version (example choosing between the different TLS versions.)
  <br /> <br />
  <img src="/img/common/protocol.png" style="width:80px;height:80px;" /> <strong>STEP 1:- Algorithms</strong>
  <br /> <br />
  Most of the technologies that are mentioned in this knowledge base are officially defined in documents called RFCs (Request for Comments).
  These are open documents that are made available by the IETF, Requests for comment (RFCs) cover many aspects of these protocols in a technical fashion.
  One can think of an RFC as a guide to implement a particular piece of technology like Network Protocols. RFCs associated with an active IETF Working Group can also be
  accessed from the Working Group's web page via IETF Working Groups ( <a href="https://datatracker.ietf.org/wg/">https://datatracker.ietf.org/wg/</a>).
  <br /> <br />
  These protocols could have flaws or vulnerabilities that usually go unnoticed for a while after it first gets published. If a flaw has been found in the protocol's official
  definition (documented in RFCs), the vulnerabiltity can be categorized as a 'Protocol Flaw'. What this means is that every implementation of the technology as per the
  RFC is likely to have introduced the same flaw in their implementation.
  <br /> <br />
  For example, the infamous Poodle vulnerability found in SSL3.0.  While SSL 3.0 is an old encryption standard and has generally been replaced by TLS, most SSL/TLS implementations
  remain backwards compatible with SSL 3.0 to interoperate with legacy systems in the interest of a smooth user experience. Even if a client and server both support a version of
  TLS the SSL/TLS protocol suite allows for protocol version negotiation (being referred to as the “downgrade dance” in other reporting). The POODLE attack leverages the fact that
  when a secure connection attempt fails, servers will fall back to older protocols such as SSL 3.0. An attacker who can trigger a connection failure can then force the use of SSL
  3.0 and attempt the new attack.
  <br /> <br />
  <img src="/img/common/implementation.png " style="width:100px;height:100px;" /> <strong>STEP 2:- Implementation</strong>
  <br /> <br />
  While protocol's official definitions make up RFCs, implementation of the definition is left to the whoever chooses to use the protocol. And if an implementor introduces
  bugs in the way the protocol was written in code, it can be termed as an "Implementation Flaw". Specifically, in software development, a lot of network protocols come as
  part of ready to be used packages called libraries. Libraries are simply imported into the code by developers to make development easier.  However, it should be noted that there
  have been some major bugs that lead to critical vulnerabilties in these libraries and as a result, exposing the product to the same.
  <br /> <br />
  For example, The Heartbleed Bug is a serious vulnerability in the popular OpenSSL cryptographic software library. This weakness allows stealing the information protected,
  under normal conditions, by the SSL/TLS encryption used to secure the Internet. The Heartbleed bug allows anyone on the Internet to read the memory of the systems protected
  by the vulnerable versions of the OpenSSL software. This compromises the secret keys used to identify the service providers and to encrypt the traffic, the names and passwords
  of the users and the actual content. This allows attackers to eavesdrop on communications, steal data directly from the services and users and to impersonate services and users.
  <br /> <br />
  It should also be noted that bugs such as Heartbleed do not indicate that one should roll out their own crypto!
  <br /> <br />
  <img src="/img/common/configuration.jpg " style="width:110px;height:100px;" /> <strong>STEP 3:- Configuration</strong>
  <br /> <br />
  A lot of protocols provide configruable options in their official definitions (RFCs). These options affect the way the protocol functions post deployment.
  It is important to be aware of the pros and cons including security implications of different configurable parameters. If a protocol is configured with an option that is
  considered to weaken security, it could result in a compromise of the product that relies on the protocol. Sometime, it is important to understand that configurable options
  are provided with protocols for reasons such as backward compatbility.
  <br /> <br />
  For Example:- TLS gives a multitude of options of Ciphers that can be used. There are some that are recommended and there are some that needs to be avoided. Certain type of ciphers
  known as DHE ciphers are safe to use only if dh group 14 (2048 bit) key sizes are being used for key exchange. If a lower dh group size is used with DHE ciphers then your server
  will be susceptible to the logjam attack.
  This means that if DHE ciphers are used, one MUST configure it as a dh group 14 (2048 bit) and nothing lower than that.
</p>
