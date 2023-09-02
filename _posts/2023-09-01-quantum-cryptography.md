---
layout: blog_post
title: "The Future of Cryptography in the Age of Quantum Computing"
categories: blog
author: "Debra Baker, Scott Fluhrer, Mike Ounsworth, and Zaid Khaishagi"
type: blog
img_tag: <img src="/img/quantum-cryptography.jpg" class="blog-photo">
# img: img/lock-icon.ico
---

<hr />

No doubt you are one of the many IT, business, policy, or other professionals who worry about security. You may have heard that when quantum computing becomes a reality all our current _cryptography_, the math behind the encryption and authentication that secures our digital worlds, will be broken; communications will be intercepted, bank accounts will be raided, and government secrets will be exposed on the Internet. The truth, fortunately, is less dire.

This paper will help explain what the coming quantum computing revolution actually means for you. Some people have started to panic and may be coming to you for advice. The _Crypto Done Right_ organization has written this paper to help answer your quantum security questions. If you are worried about the threat of quantum computing, you needn't be.

**Key Takeaways:**

-   Quantum computing is unlikely to be an issue for at least 10 years

-   In the post-quantum computing world, good security practices such as regular patching/updating will still be a critical part of your security strategy

-   Cryptographers are currently working on new algorithms that are not vulnerable to quantum computing

-   An appropriate response is measured with caution. IT administrators need to make sure that the systems their organization uses remain up to date. Developers working on future software and firmware should take the implications of quantum computing into consideration. Managers need to know how and where their security data is kept and have a security migration plan.



<h2 style="color:#2f5496;"><strong>Future of Cryptography in the Age of Quantum Computing</strong></h2>

For most organizations, top security concerns now and in the future remain strong password policies, maintaining up-to-date system patches on their network, and ensuring users don't click on links in their emails. These same concerns will still exist even after quantum computing is developed.

Looking ahead, when quantum computing matures it will radically disrupt current cryptography. This document provides a brief overview of the threats of quantum computing. We want to emphasize that the most pressing security concerns today will also be concerns in the post-quantum computing world.


<h3 style="color:#2f5496;"><strong>Brief Overview of How Quantum Computing Will Eventually Break Current Cryptography</strong></h3>

Modern cryptography fulfills many different functions. The most common is _encryption_, which is used to keep data confidential. But there are many other operations that are equally as important. One such operation is securely creating temporary one-time keys needed when two computers talk to each other[^1]. Another critical cryptography operation is a process that allows a website to verify its identity.

These different operations function together to make internet security work. For example, when you connect to your online banking website, your browserand the bank's webserver perform a special secure exchange of data, called a handshake to set up secure communications.

The purpose of the handshake is to enable the exchange of encrypted and authenticated data back and forth between your browser and your bank's webserver. To create this secure connection your browser and the bank webserver share a one-time key. The browser confirms it is sharing the one-time key with the real bank and not an imposter by validating the bank's security certificate.

Each of these steps is performed by a different set of cryptographic algorithms, as follows:

- The encrypted/authenticated messages are created using symmetric algorithms[^2]. Systematic algorithms use the same key for both your browser and the bank's webserver.

- The one-time key is generated using an asymmetric algorithm[^3]. Asymmetric algorithms require both your browser and the bank's webserver to create public data and private data. They then exchange their respective public data. Your browser's private data combined withthe bank's webserver public data produces the same output as the bank's private data combined with your browser's public data. Because both computers have generated the same output, that output can be used to generate the same one-time key on both sides.

- A signed certificate is a piece of publicly available digital data that verifies web site identities. A certificate is verified by another asymmetric process. This certificate is used to verify that the server that is answering is genuine. The bank's private key is used to generate a digital signature for the bank's certificate. Your browser uses a known public key associated with the bank's website to verify that the certificate is valid for your bank.

Let's now explore the relationship of what we just discussed with quantum computing. Consider that asymmetric algorithms used today will be rendered ineffective by adequately powerful quantum computers of sufficient size. Asymmetric algorithms are based on certain mathematical formulas, and these formulas make it relatively easy to derive a public key from the private key, but not the other way around, making it hard to compute the private key from the public key. With current computers, it would literally take hundreds of millions of years to crack the public/private key pairs in use.

The attraction of quantum computers is that they will be able to perform certain computations many times faster than current computers. That means that asymmetric algorithms will be much easier for quantum computers to figure out. A sufficiently powerful quantum computer could crack many current keys in hours or even minutes[^4]. These asymmetric algorithms will need to be replaced.

Therefore, If a hacker had a powerful quantum computer, they could forge asymmetric private keys. This would enable them to sign certificates for any website they wanted. The hacker would be able to forge a valid certificate for any website. It would be impossible to know if a website was real or fake.

Alternatively, a hacker could forge the private data for an asymmetric key exchange. The hacker could generate the same one-time key as the browser and webserver. Using this forged key, the attacker could decrypt secure communications between a web browser and a webserver and/or insert their own fake messages.

Quantum computing also threatens symmetric algorithms. Symmetric algorithms are not based on mathematical formulas that can be easily computed. Symmetric keys are random sequences of data. When symmetric keys are created correctly, a hacker would have to try every possible key value to find the right one. This is called a brute force attack. Quantum computers[^5] can perform brute-force attacks much more quickly than current computers.

Fortunately, cryptography is more complicated than simply storing keys. Searching for a 128-bit key takes a very long time. Using more processors decreases the time, but even quantum computers will likely not be powerful enough to brute force attack a 128-bit key, the most common length of keys. And 256-bit long keys are certainly secure from quantum computers.

In the meantime, cryptographers are working on new asymmetric algorithms that are not vulnerable to quantum computing. The most popular asymmetric algorithms in use today are based on two mathematical algorithms and both are vulnerable to quantum computers.

The new algorithms using enhanced mathematical formulas will not be susceptible to quantum computers. These new algorithms will be quantum-resistant.

Currently, a number of algorithms are being evaluated by the cryptographic community, and several are moving toward standardization. Therefore, by the time quantum computers are powerful enough to break our current cryptography, we should already have in place new algorithms that are not vulnerable to it.

<h3 style="color:#2f5496;"><strong>Concerns for Developers, Managers, and IT Administrators</strong></h3>

What does this mean for you today? The answer to that question depends on your current role.


### a.  Developers

Going forward software and firmware need to be developed with the future implications of quantum computing taken into consideration. Applications such as banking systems, industrial controls, embedded systems, medical devices, etc. which are intended for long-term usage are often not easy to update in the field. For these systems, it is not too early to start putting measures in place that can weather the impact of quantum computing. Ideally, devices should support field-upgradable firmware, including a mechanism to update cryptographic modules and trusted root keys used to verify firmware updates. Where field upgrades are not possible, device manufacturers should start signing firmware with one of the standard hash-based signature algorithms. NSA wants all new applications to be using XMSS or LMS for firmware signing starting in 2025.

### b.  Managers

It is also important to know where and how cryptography is used in your organization. Especially when it comes to data handling and storage. Smart ID badges and Wi-Fi authentication also use cryptography. Taking a careful inventory now will make it easier to migrate to quantum-resistant algorithms and standards when they become available. It is also important to have a security migration plan in place. Migrating the security process can be among the most high-risk projects at any organization.

### c.  Administrators

For IT admins, the most important current concern is ensuring that the systems used by the organization are up-to-date and follow the appropriate standards and guidelines. IT Administrators should also conduct detailed security and cryptography audits.

<h3 style="color:#2f5496;"><strong>What will matter <i>then</i> already matters <i>now</i></strong></h3>

Security experts and cryptographers are already working on enhanced algorithms. It is likely that the new algorithms will be available before quantum computers mature. Future security and encryption software will have similar problems as we deal with today. Users resist updating their computers. This updating process is becoming easier to automate. However, there is still a need for manual updating. In fact, the Equifax hack in 2017 happened, in part, because of an unpatched server. New algorithms will do you no good if you do not patch and update your systems.

Passwords are another constant problem which is all the more problematic because many of our cryptographic keys are derived from or protected by passwords in one form or another. Doubling the size of symmetric keys will not solve the password problem. A post-quantum computing bad password will be just as insecure as a bad password is now.

Despite advanced cryptographic measures, social engineering will remain a significant threat. , so if our systems are being compromised by phishing emails now, they will continue to be compromised in the post-quantum computing world. Quantum-resistant certificates and signatureswon't stop a user from clicking on unverified links in an email.

The point we are making here is that most users don't need to worry about quantum computers. It's more important to figure out improved systems security right now. Quantum computing isn't going to matter for many more years. By the time it does, if you have developed good security deployments and operations, you will be able to make a smooth switchover. Much like the Y2K bug, you'll be more aware of the news reports around quantum computers than you will experience any significant problems.


**If after reading this article you still have questions, please reach out. We at Crypto Done Right will be happy to help answer them!**

---

[^1]: More typically, two keys, one to encrypt client-to-server traffic, and one to encrypt server-to-client traffic.

[^2]: Such as AES. Technically, there is a bit more happening here to provide the authentication, but that is left out for simplicity.

[^3]: Called Diffie Hellman or DH. Many modern systems use a variant called Elliptic Curve Diffie Hellman, or ECDH.

[^4]: Using Shor's Algorithm. Named for Peter Shor.

[^5]: Using Grover's Algorithm. Named for Lov Grover.