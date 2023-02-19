---
layout: page
title: SSL 2.0
type: cryptographic_protocols
update: Last Updated Fri, 3 May 2019 19:37:01 -0400
permalink: /articles/cryptographic_protocols/ssl_v2.html
alerts:
  - id: 1
    type: danger
    description: Warning! This technology is obsolete!
further-reading:
  - name: Analysis of SSL
    link: https://www.schneier.com/academic/paperfiles/paper-ssl.pdf
  - name: Disabling SSLv2 and SSLv
    link: https://support.globalsign.com/customer/portal/articles/2356063
attacks:
  - name: DROWN Vulnerability
    description: ": DROWN (Decrypting RSA using Obsolete and Weakened eNcryption) allows attackers to break the encryption and read or steal sensitive communications,
       including passwords, credit card numbers, trade secrets, or financial data."
    link: ""
  - name: Ciphersuite RollBack Attack
    description: ": An attacker is able to modify the SSL Handshake to force the connection to use weaker cipher suites than what the client has proposed.
    SSLv2 has a lot of weak encryption ciphers available. It is not uncommon to find weak encryption settings enabled on a server. One such weak encryption algorithm is named DES."
    link: ""

---
SSL 2.0 was officially the first SSL version available (SSLv1 never got released). It was released in February 1995.
A lot of weaknesses in the protocol led to the development of SSLv3.0. A lot of modern systems do not support SSL2.0 so supporting it for whatever reason would be a major security concern and is simply not recommended.
