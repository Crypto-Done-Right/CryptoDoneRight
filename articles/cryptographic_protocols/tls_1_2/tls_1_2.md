---
layout: page
title: TLS 1.2
type: cryptographic_protocols
update: Last Updated Thu, 12 Dev 2018 12:00:01 -0400
permalink: /articles/cryptographic_protocols/tls_1_2/tls_1_2.html
alerts:
  - id: 1
    type: danger
    description: TLSv1.2 is secure only when it is configured properly!
    link: ""
best_practices:
  - name: "TLS 1.2 uses Auth-then-Encrypt, or MAC-then-Encrypt, which is known to be vulnerable"
    description: "Check out the RFC for Encrypt-then-Auth. note: this is addressed in TLS 1.3, so upgrade if you can!"
    link: https://tools.ietf.org/html/rfc7366
further-reading:
  - name: "RFC 8446: The Transport Layer Security (TLS) Protocol Version 1.2"
    link: "https://www.ietf.org/rfc/rfc5246.txt"
has_faq: yes
---
<p> TLSv1.2 is a revision to the TLSv1.1 and was released in August of 2008. Just like previous revisions to TLS, this revision aims at improving the security of the protocol by improving the encryption and hashing standards. One of the primary goals of the TLS 1.2 revision was to remove the protocol’s dependency on the MD5 and SHA-1 digest algorithms.</p>
