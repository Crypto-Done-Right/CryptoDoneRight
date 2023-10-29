---
layout: blog_post
title: "You Should Care About Quantum Cryptography"
categories: blog
author: "Debra Baker, Scott Fluhrer, Mike Ounsworth, Zaid Khaishagi, and Kayla Grigg"
type: blog
img_tag: <img src="/img/blogs/quantum-cryptography-2-logo.jpg" class="blog-photo">
# img: img/lock-icon.ico
---

<hr />

If you’re worried (or even just curious!) about data security and quantum computing, you’re not alone. Many IT, business, policy, and other professionals are concerned about the impact of quantum computing.

You may have heard that when quantum computing becomes a reality, all of our current cryptography — _that is, the math behind the encryption and authentication that secures our digital worlds_ — will be broken. Communications will be intercepted, bank accounts will be raided, governments and private citizens alike will have all of their secrets disgorged and promulgated all over cyberspace… _“Dogs and cats living together, MASS HYSTERIA!”_[^1]

The rumors you’ve heard likely painted a pretty bleak, dystopian picture. And you’re probably wondering what the coming quantum revolution means in practice — for you, for your organization, even for the world. 

Well, Crypto Done Right is here to help! 

In this article, we’ll explain how current cryptography works and why quantum computing poses a threat. Then, we’ll discuss specific concerns for both developers and managers. Finally, we’ll share what you can do now to prepare yourself and your organization for the coming quantum revolution.

### This Is (Not) the Perfect Time to Panic!

Before we dive in, let’s make one thing clear: If you’re worried about what’s sometimes called the “post-quantum world,” there’s no need to panic. And if you’re being pressured or questioned by others (say, your boss) because of their post-quantum worries, you can tell _them_ not to panic!
Here’s why:


-   Quantum computing is unlikely to be an issue **until 2033 or later**

-   If you’re already following good security practices, such as regular patching/updating, you’ll likely be protected when the post-quantum world arrives

Cryptographers and other qualified professionals are already working on new algorithms that are not vulnerable to quantum computing.

All that said, when quantum eventually matures, it will disrupt current cryptography.  So how are you supposed to prepare?


<!-- <h2 style="color:#2f5496;"><strong>Future of Cryptography in the Age of Quantum Computing</strong></h2> -->
### What Can You Do Now?

Before we dive into the details of cryptography and quantum computing, rest assured there are steps you can take to prepare your organization for quantum when it comes. We’ll cover these in more detail later in this paper, but here’s a quick preview of what IT admins, developers, and managers can do now: 

-   **IT Admins:** Make sure the systems your organization uses are up-to-date

-   **Developers:** For those working on long-lasting software and firmware, take into consideration the future implications of quantum computing while developing products

-   **Managers:** Know how and where your data is kept and have a migration plan

Now let’s take a look at how quantum will impact current cryptography.

<!-- <h3 style="color:#2f5496;"><strong>Brief Overview of How Quantum Computing Will Eventually Break Current Cryptography</strong></h3> -->

## How Quantum Computing Will Eventually Break Current Cryptography: A Brief Overview

In modern computer security, including for the Internet, cryptography performs a variety of functions. The most obvious to many people is _encryption_, which is generally used to keep data confidential.  But there are many other operations that are _at least_ as important… and maybe even more so.

For example, cryptography is used to securely create a temporary, one-time key every time two computers want to talk to each other.[^2] It’s also used when one computer determines the identity of another computer it is talking to. 

That last one is really important. Consider how unhappy you would be if you accessed a website that looked exactly like your bank — complete with logins, money transfers, etc. — but was _actually_ a criminal website posing as your bank. Thanks to cryptography, however, you can ensure the sites you access are legitimate.

Together, these cryptographic operations make Internet security work. 

### It’s All in the Handshake—How you know who you’re talking to

Let’s keep using your online banking website as an example. First, your browser and the bank’s web server will do a special exchange of data called a _handshake_ to set up secure communications. In basic terms, the handshake process goes like this:

1. BROWSER: Hello, www.YourBank.com. Please prove that you really are “YourBank.” And, while we’re at it, I’m sending the necessary data to generate a one-time cryptographic key to talk to you securely.

2. WEB SERVER: Hello, browser. I’m sending you a signed certificate that proves I am “YourBank”. I’m also sending data for generating a one-time key.

3. BROWSER and WEB SERVER both generate the same one-time key using the data they exchanged with each other, which will be used to encrypt and decrypt messages sent between them. 

4. BROWSER: OK, YourBank, I’m sending you an encrypted, authenticated message. If you can read this, we are sharing the one-time key we generated. Now if anyone modifies the message, the YourBank computer can tell.

5. WEB SERVER: OK, here is my encrypted, authenticated message. If you can read this, we are sharing the one-time key we generated.

![](/img/blogs/quantum-cryptography-2.png)

### The Algorithms Behind Computer Security

The ultimate goal of the handshake is to be able to send encrypted and authenticated messages back and forth (as depicted in steps four and five). To do that, the browser and web server have to share the one-time key. At the same time, the browser must confirm that it is sharing the one-time key with the real bank and not an imposter. 

Believe it or not, each of these steps is performed by a different cryptographic algorithm. Let’s take a brief look at each of these algorithms. 

-   Advanced Encryption Standard (AES): Encrypted and authenticated messages are created using symmetric algorithms like AES[^3]. These algorithms are called “symmetric” because they use the same key for both the browser and the web server.

-   Diffie Hellman (DH): The one-time key in our example is generated using an asymmetric algorithm called Diffie Hellman or DH[^4]. This algorithm is called “asymmetric” because both the browser and the web server create _**public data**_ and _**private data.**_ Each sends the other their respective public data. The DH algorithm uses clever mathematics and has an amazing property that the browser’s _**private data**_ combined with the web server’s _**public data**_ produces the same output as the web server’s _**private data**_ combined with the browser’s _**public data**_. Now, no one just looking at the public data can figure out what that output is. Because both computers have generated the same output, it can be used to generate the same one-time key on each side.

-   Rivest, Shamir, Adleman (RSA): Finally, a signed certificate, which is a piece of publicly available information that can be used to verify identities, is verified by another asymmetric process. The most commonly used algorithm is Rivest, Shamir, Adleman, or RSA. The certificate is used to verify that the server that is answering is, in fact, YourBank. Although the full details are not described here, the important steps are that a _**private key**_ is used to generate a digital signature for the certificate. The browser uses a known _**public key**_ to verify that the certificate is valid and authorized for the correct website.

### Quantum Computing vs. Asymmetric Algorithms

So, what does quantum have to do with all of this? Well, it depends on the algorithm being used. 

The standard asymmetric algorithms used in the handshake process will be completely broken by a functional quantum computer of sufficient size and reliability.

That’s because asymmetric algorithms are based on certain kinds of “tricks” in math, wherein it is easy to compute in one direction but hard to compute in the reverse. For example, it is easy to derive a public key from the private key, _but not the other way around_. It is hard to compute the private key. And when we say “hard,” we mean it should take somewhere on the order of _hundreds of trillions of years_ to crack some of these keys with classical (that is, non-quantum) computing.

The problem is, that the math upon which these two types of algorithms are based is much less difficult for quantum computers to figure out. A sufficiently powerful quantum computer could break these kinds of algorithms in hours or even minutes using another algorithm known as Shor’s Algorithm.

Or, said another way, if an attacker had a powerful enough quantum computer, they could forge the asymmetric private key or data. This would enable them to sign and present valid certificates for any website on the Internet. It would be impossible to know if the website you were browsing was real or fake. That might not matter for visiting a gaming website, but nobody would be able to bank, shop, or even browse news stories online with confidence.

But that’s not the only way quantum computing could create problems in the handshake process. The attacker could also forge the private data for the Diffie Hellman key exchange. This means that the attacker could generate the same one-time key as the browser and web server. Using this same key, the attacker could decrypt all messages and/or insert their own fake messages.

Ultimately, the result is the same:  **If quantum computers become sufficiently powerful, these algorithms will simply have to be retired.**

### Quantum Computing vs. Symmetric Algorithms

Quantum computing weakens the symmetric algorithm as well, but not nearly as much. There is no mathematical trick that can easily be computed — and exploited. Symmetric keys are effectively random sequences of data. When created correctly, an attacker would have to try every possible key to find the right one. This is called a brute force attack.  Compared with our current computers, a quantum computer using an algorithm called Grover’s Algorithm can perform brute-force attacks far more quickly. 

However, it turns out to be more complicated than that — and that’s a good thing since higher complexity means things are more secure than they seem at first glance. As it turns out, Grover’s Algorithm takes a _huge_ amount of time to search for a 128-bit key[^5], and throwing more processors at the problem actually _lessens_ the advantage that Grover’s Algorithm gives. 

The bottom line? In a post-quantum world, 128-bit AES keys are likely to be secure…  and 256-bit AES keys are _certainly_ secure.


### Quantum Resistant Algorithms

In the meantime, cryptographers from around the world are working on new asymmetric algorithms that are not vulnerable to quantum computing, and specifically Shor’s Algorithm. That’s because currently, all of our most popular asymmetric algorithms are based on two fundamental problems (or “tricks”), and both of these problems happen to be vulnerable to Shor’s Algorithm.

Fortunately,  Shor’s Algorithm does not easily solve _all_ mathematics problems, just the mathematical problems on which our current asymmetric cryptography is based. So cryptographers are working on developing new algorithms that use different mathematical problems that are not easily solved by Shor’s Algorithm. We call these new algorithms “quantum resistant.”

A number of algorithms are already being evaluated by the cryptographic community right now and several are moving toward standardization. The good news is that by the time quantum computers are powerful enough to break our current cryptography, we should already be switched over to new algorithms that are not vulnerable.


## Concerns for IT Admins, Developers, and Managers

Long-lasting software and firmware need to be developed with the future implications of quantum computing taken into consideration. 

Of course, these changes are more urgent for certain industries. Applications such as banking systems, industrial controls, embedded systems, medical devices, etc. which are intended for long-term usage are often not easy to update in the field. **For these systems, it is not too early to have measures in place that can weather the impact of quantum computing.** 

Where possible, devices should support field-upgradable firmware, including a mechanism to update cryptographic modules and trusted root keys used to verify future firmware updates. 

Where field upgrades are not possible, device manufacturers should be starting to sign firmware today with one of the approved hash-based signature algorithms. — (Hint: NSA wants all new applications to be using XMSS or LMS for firmware signing starting in 2025!)

It is also important to properly **audit where and how cryptography is used in your organization**. Most often this is surrounding data handling and storage, but it may also show up in authentication such as building access ID badges or how laptops and phones authenticate to the Wi-Fi. Taking a careful inventory now will make it easier to migrate to new quantum-resistant algorithms and standards when needed. 

Along the same note, it is also important to have a migration plan in place so that the process is smooth when the time comes. Without this, migration may be haphazard and have cracks that can expose your data and systems to attacks. As such, migration plans should be a key area of focus for managers hoping to future-proof their organizations. 

For IT admins, the most important concern at this time is to **make sure that the systems used by the organization are up-to-date and follow the appropriate standards and guidelines, and to start planning for any hardware migrations identified by your crypto audits.**

### What Will Matter Then Already Matters Now
Because security experts and cryptographers are already working on replacement algorithms, it is highly likely that the new algorithms will already be available before quantum computers mature. _So, there’s nothing to worry about, right?_

Well, that depends.

If you encrypt data now (for example, have a secure connection with your bank), someone could theoretically record your encrypted connection, and then when they have a mature quantum computer, go back and decrypt it — perhaps 10 or 15 years in the future. 

However, that’s not the biggest problem we’ll face with quantum computing. 


*Problem #1*: Patching & Updating
The biggest problem for IT admins is, even if the new algorithms are available, _how many systems will they be installed on?_ Users already resist updating their computers. In fact, the Equifax hack in 2017 happened, in part, because of an unpatched server. **New quantum-resistant algorithms will do no good if you do not patch and update your systems.**

---

*Problem #2*: Passwords

Another big problem is that many of our defenses are based on passwords. Even many of our cryptographic keys are derived from or protected by passwords in one form or another. **Doubling the size of symmetric keys will not solve the password problem.** A post-quantum bad password will be just as insecure as a bad password is now. _(And yes, “p@ssw0rd” is a bad password.)_

---


*Problem #3*: Social Enginnering

Of course, social engineering bypasses all cryptographic defenses regardless of the algorithm. If our systems are being compromised by phishing emails now, they will continue to be compromised in the post-quantum world. **Quantum-resistant certificates and signatures can’t stop users from haphazardly clicking on any link that hits their inbox or giving their login data to a scammer or scam website.**


The point is that the vast majority of users shouldn’t be worrying about quantum computing and what it will do to their systems. Why? Because the biggest challenges we’ll face in a post-quantum world are challenges we’re already dealing with.

---


### Strengthen Security Today, Be Prepared for Tomorrow


Instead of worrying, take time to figure out and improve the security of your system _right now!_ Quantum computing isn’t going to matter for many more years yet. And by the time it does, if you have been developing good security deployments and operations, you may not even notice when the switchover happens. Instead, much like the Y2K bug, you’ll probably be more aware of the news reports about it than actually experiencing any significant problems.

The best thing you can do — far more than worrying about whether quantum computing is going to end the digital world — is to deal with security issues that are most likely putting you at risk right now. Ultimately, the stronger your security is now, the better positioned you’ll be when quantum computing finally matures.


**If after reading this article you still have questions, please reach out. We at Crypto Done Right will be happy to help answer them!**

---

[^1]: From the 1984 American supernatural comedy film Ghostbusters.

[^2]: Actually, it’s typically two keys: one to encrypt data traveling from your device (computer, phone, tablet, etc.) to the server, and another to encrypt data coming from the server to your device.

[^3]: Technically, there is a bit more happening here to provide the authentication, but that is left out for simplicity.

[^4]: Many modern systems use a variant called Elliptic Curve Diffie Hellman, or ECDH.

[^5]: A 128-bit key means a cryptographic key which is 128 bits in length. The key size is denoted using its bit length, and a larger key size generally means better security.