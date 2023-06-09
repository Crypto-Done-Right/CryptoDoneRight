---
layout: page
title: SSL 3.0
type: cryptographic_protocols
update: Last Updated Fri, 3 May 2019 19:45:00 -0400
permalink: /articles/cryptographic_protocols/ssl_v3.html
alerts:
  - id: 1
    type: danger
    description: "Warning! This technology is obsolete!"
further-reading:
  - name: Analysis of SSL
    link: "https://www.schneier.com/academic/paperfiles/paper-ssl.pdf"
  - name: Disabling SSLv3
    link: "https://disablessl3.com/"
  - name: "SSL/TLS: A Beginner's Guide"
    link: "https://www.sans.org/reading-room/whitepapers/protocols/paper/1029"
  - name: Analysis of the SSL 3.0 protocol
    link: "https://www.schneier.com/academic/paperfiles/paper-ssl-revised.pdf"
related-articles:
  - name: RFC for Disabling SSLv3
    link: "https://tools.ietf.org/html/rfc7568#section-5"
  - name: Disabling SSLv2 and SSLv3
    link: "https://support.globalsign.com/customer/portal/articles/2356063"
attacks:
  - name: POODLE
    description: ": The attack that killed off SSLv3.0. POODLE allows an attacker to force a SSLv3 connection and use weak configuration to break security."
  - name: BEAST
    description: ": A vulnerability that can be exploited using browsers (HTTPS). A client side attack whose possible impacts include session hijacking."
  - name: Logjam
    description: "An easy to exploit vulnerability if weak configuration is used. This vulnerability affects all versions of SSL/TLS."
  - name: ROBOT
    description: "A weakness in the RSA encryption standard known as PKCS#1v1.5 that can ultimately allow an attacker to learn a secured website’s private key in a relatively short amount of time."
    link: "https://robotattack.org/"

---
SSL stands for Secure Sockets Layer and was originally created by Netscape. It is used for providing confidentiality, authenticity and integrity by establishing an encrypted link between a server and a client. This link ensures that all data passed between the web server and browsers remain private and integral. SSLv2 and SSLv3 are the 2 versions of this protocol (SSLv1 was never publicly released). After SSLv3, SSL was renamed to TLS. Those protocols are standardized and described by RFCs.
