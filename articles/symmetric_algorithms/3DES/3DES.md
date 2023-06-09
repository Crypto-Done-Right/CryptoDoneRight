---
layout: page
title: 3DES
type: symmetric_algorithms
update: Last Updated Tues, 27 Aug 2019 12:00:01 -0400
permalink: /articles/symmetric_algorithms/3des/3des.html
alerts:
  - id: 1
    type: danger
    description: This is the NOT the recommended standard.
    link: /articles/symmetric_algorithms/aes/aes.html
  - id: 2
    type: danger
    description: There are serious security implications if not configured properly!
    link: ""
  - id: 3
    type: danger
    description: "3 DES is now officially retired!"
    link: https://www.cryptomathic.com/news-events/blog/3des-is-officially-being-retired
further-reading:

related-articles:
has_faq: yes
attacks:
  - name: Meet in the Middle Attack
    description: ":This particular attack can occur with specific settings in which DES could operate (keying option 1)."
    link: ""
  - name: Sweet 32
    description: This is a major attack that renders 3DES weak and compromises the security entirely. But like mentioned before, there are ways to mitigate and still use 3DES. OpenSSL does not include 3DES per default since version 1.1.0 (August 2016), and considers it a "weak cipher". Cisco's advisory on Sweet32:"
    link: "https://www.synopsys.com/blogs/software-security/sweet32-retire-3des/"

---
The Triple Data Encryption Algorithm, called 3DES for short, is an encryption algorithm that evolved from previous flavors of the same algorithm (Data Encryption Standard, or DES, which was first published in 1975). Although under certain configurations 3DES can be acceptable, it is being phased out slowly as there are new vulnerabilities that make the protocol significantly weaker. Where possible, newer standards such as AES should be used; there are no reasons to stick to 3DES apart from backward compatibility or legacy support.
