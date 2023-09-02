<!-- ---
layout: blog_post
title: "The Future of Cryptography in the Age of Quantum Computing"
categories: blog
author: "Seth Nielson"
type: blog
img_tag: <img src="/img/quantum-cryptography.jpg" class="blog-photo">
# img: quantum-cryptography.jpg
---

<hr />

If the title of this article managed to catch your attention, there is a
good chance you are one of the many IT, business, policy, or other
professionals that worry about security. And there is a good chance that
you have heard that when quantum computing becomes a reality, all of our
current *cryptography*, the math behind the encryption and
authentication that secures our digital worlds, will be broken.
Communications will be intercepted, bank accounts will be raided, while
governments and corporations will have all of their secrets disgorged
and promulgated all over cyberspace (some people might like that last
one).

"*Dogs and cats living together, mass hysteria!*"[^1]

For whatever reason, you have become concerned about what the coming
quantum revolution means for *you*. Or, maybe other people, like your
boss, have started to panic and are coming to you for advice. Or, maybe
you're just curious. Either way, you would like to know what it all
means in practice.

Well, Crypto Done Right is here to help!

First and foremost, if you are worried about what is sometimes called a
"post quantum world," you can relax! And if you are being pressured or
questioned by others that worry about a post-quantum world, you can tell
them to relax!

The short version is this:

-   Quantum computing is unlikely to be an issue for **at least** 10 years

-   Whenever the post quantum world arrives, users that already practice good security by ***regular patching/updating*** will probably already be protected

There are some exceptions, if you are an OEM manufacturer that
implements your own crypto in hard-to-patch devices in the field (for
example if crypto is implemented in silicon or a TPM co-processor). For
these people, they need to start the migration to Post Quantum (PQ) one
full device lifecycle before quantum computers become a reality. For
most people in this category, they are already too late.

OEM manufacturers that implement your own crypto in easy-to-patch
devices or software in the field. Here you need to have your PQ-enabled
patches deployed before quantum computers are real. The magic trick here
is that they will probably be real \~ 2 years before the public knows
that they are real. Most companies have a couple-year R&D lead time on a
major change like this, so up to you how early you start.

In fact, if you want to worry about *something*, please take this to
heart:
> *Any time you are currently spending worrying about whether quantum computing is going to end the digital world is time that would be better spent dealing with **security issues that are most likely putting you at risk <u>right now</u>!***<

So, if you want to spend some time worrying about the security of your
organization, please start with whether or not your users are using
"p@ssw0rd" as their password, have unpatched systems on your network,
and uncritically click on links in their emails. Please note, *you will
still need to deal with these issues even after quantum computing comes
around so you might as well start now!*

Still, you came here to learn a little bit about quantum and how, when
it eventually matures, it will disrupt current cryptography. So, to
indulge you, we will provide a brief overview. Then, to reinforce the
main point of this article, we will give some examples of why the
security issues that are more pressing concerns *right now* will also be
the pressing concerns *even in the post quantum world*!

## <u>A Brief Overview of How Quantum Will <i>Eventually</i> Break Current Cryptography</u>

In modern computer security, including for the Internet, cryptography
has to provide a lot of different functions. The most obvious to many
people is *encryption*, which is generally used to keep data secret (or
"confidential" as cryptographers say). But there are many other
operations that are at least as important and maybe more so. One is a
mechanism that is used to securely create a temporary, one-time key
every time two computers want to talk to each other.[^2] Another is a
process whereby one computer proves its identity of the other computer
it is talking to. That last one is really important. You would be really
sad, for example, if you thought you were accessing a website that
looked like your bank (complete with logins, money transfers, etc) but
was actually a criminal website that just looks like your bank.

These different operations are combined together to make Internet
security work. So, using your online banking website as an example, your
browser and the bank's webserver will do a special exchange of data,
called a "handshake," to setup secure communications. The following is a
much simplified process that describes the handshake:

1.  BROWSER: Hello, www.somebank.com. Please prove that you really are "somebank." And, while we're at it, I'm sending the necessary data to generate a one-time key to talk to you securely. ![](/img/quantum-cryptography-1.png)

2.  WEBSERVER: Hello, browser. I'm sending you a signed certificate that proves I am "somebank". I'm also sending data for generating a one-time key.

3.  BROWSER and WEBSERVER both generate the same one-time key using the data they exchanged with each other. (No other computer can do so).

4.  BROWSER: \{\{OK, somebank, I'm sending you an encrypted, authenticated message. If you can read this, we are sharing the one-time key we generated. Now if anyone modifies the message, the somebank computer can tell\}\}

5.  WEBSERVER: \{\{OK, here is my encrypted, authenticated message. If you can read this, we are sharing the one-time key we generated.\}\}

Each of these steps was necessary. The ultimate goal of the handshake is
to be able to send encrypted and authenticated messages back and forth
as depicted in steps 4 and 5. But to do that, the browser and webserver
have to share the one-time key. And, at the same time, it is essential
that the browser confirm it is sharing the one-time key with the real
bank and not an imposter.

Also, each of these steps is performed by a different cryptographic
algorithm.

-   The encrypted/authenticated messages are created using symmetric algorithms like AES[^3]. These algorithms are called "symmetric" because they use the same key for both the browser and the webserver. In the example, both the browser and the webserver must generate the same key for this to work.

-   The one-time key is generated using an asymmetric algorithm called Diffie Hellman or DH.[^4] This algorithm is asymmetric because both the browser and the webserver create ***public*** data and ***private*** data. Each sends the other their respective public data. The DH algorithm uses clever mathematics and has an amazing property that the browser's ***private*** data combined with the webserver's ***public*** data produces the same output as the webserver's ***private*** data combined with the browser's ***public*** data. Now no one just looking at the public data can figure out what that output is. Because both computers have generated the same output, it can be used to generate the same one-time key on each side.

-   Finally, a ***signed*** certificate, which is a piece of publicly available information that can be used to verify identities, is verified by another asymmetric process;; this certificate is what is used to verify that the server that is answering is, in fact, somebank. Although the full details are not described here, the important steps are that a ***private key*** is used to generate a digital signature for the certificate. The browser uses a known ***public key*** to verify that the certificate is valid and authorized for the correct website.

So, what does quantum have to do with all of this? Well, it depends on
the algorithm. The standard asymmetric algorithms used in this process
will be completely broken by a functional quantum computer of sufficient
size and reliability.

In more detail, asymmetric algorithms are based on certain kinds of
"tricks" in math, often called "trapdoor functions", wherein it is easy
to compute in one direction but "hard" to compute in the reverse.
Because of algorithms which implement such "tricks", it is easy to
derive a public key from the private key, ***but not the other way
around***. It is "hard" to compute the private key. And to give you an
idea of how "hard," it should take somewhere on the order of ***hundreds
of trillions of years*** to crack some of these keys with "classical"
(non-quantum) computing.

Another way of understanding 128 bits of security is to Imagine I have a
grain of sand, it\'s my special secret grain of sand.

I go hide it among the \~ 7.5 sextillion grains of sand on Earth \[gives
us \~ 62 bits of security\]

Actually, scratch that, I hide it on one of the 100 billion planets in
the milky way galaxy. \[gives us another 37 bits, for a total of 99
bits\].

You are still 500 million times more likely to find my grain of sand
within your lifetime than to crack my crypto key with 128-bits of
security. Of course computers with big graphics cards speed this up, but
not enough to make a difference \... until quantum computers enter the
scene!

The problem is, it turns out that the math upon which these two types of
algorithms are based is much less "hard" for quantum computers to figure
out. A sufficiently powerful quantum computer could break these kinds of
algorithms in hours or even minutes using "Shor's Algorithm."[^5] In
short, the algorithms themselves will have to be replaced.

Or, said another way, if an attacker had a powerful enough quantum
computer, they could forge the asymmetric private key or data. This
would enable them to sign certificates for any website they wanted. The
attacker would be able to present a valid certificate for any website on
the Internet. It would be impossible to know if the website you were
browsing was real or fake. That might not matter for visiting a news
website, but nobody would be able to do online banking. Since ECDSA keys
are used to protect bitcoin wallets, you could take over anyone's
bitcoin wallet.

Alternatively, the attacker could forge the private data for the Diffie
Hellman key exchange. This means that the attacker could ***generate the
same one-time key as the browser and webserver.*** Using this same key,
the attacker could decrypt all messages and/or insert their own fake
messages.

In other words, if we get sufficiently powerful quantum computers, these
algorithms will simply have to be retired.

Quantum computing also weakens the symmetric algorithm as well but not
nearly as much. There is no mathematical trick that can easily be
computed. Symmetric keys are (or are supposed to be) effectively random
sequences of data. When created correctly, an attacker would have to try
every possible key to find the right one. This is called a brute force
attack. With quantum computers, using "Grover's Algorithm,"[^6] a
quantum computer can perform brute-force attacks more quickly,
potentially breaking a key of 128 bits in the time it would take to
search through 64 bits of key space (the square root of the original
time). However, it turns out to be more complicated than that (and in
this case, the complication means things are more secure than at first
glance). To search for a 128 bit key, it turns out that Grover's
algorithm takes a huge amount of time (and throwing more processors at
the problem lessens the advantage that Grover's algorithm gives). The
bottom line behind this is that 128 bit AES keys are likely to be
secure, and 256 bit AES keys are certainly secure.

In the meantime, cryptographers from around the world are working on new
asymmetric algorithms that are not vulnerable to quantum computing (and
specifically, Shor's algorithm). It turns out for all of our currently
most popular asymmetric algorithms are based on two fundamental problems
(or "tricks"), and both these problems are vulnerable to Shor's
algorithm.

But Shor's algorithm does not easily solve ***all*** mathematics
problems, just the mathematical problems on which our current asymmetric
cryptography is based.

Anyone who has built a gaming PC knows that Graphics Processing Units
(GPUs) are powerful processors, but they only excel at a very narrow
type of problem: ray tracing millions of pixels in parallel. For most
types of computation, like computing pi or running the macros on your
massive spreadsheet, GPUs perform much worse than a regular CPU.
Similarly, quantum computers excel at making statistical guesses about
data that looks a bit like a wave; ie data that has a lot of repetition.
It just so happens that all the asymmetric crypto that we use today is
based on equations with a high degree of repetition and therefore fall
neatly into the type of problem that quantum computers are good at
solving. Oops.

So cryptographers are working on developing new algorithms that use
different mathematical problems that are not easily solved by Shor's
algorithm. We call these new algorithms quantum resistant.

A number of algorithms are already being evaluated by the cryptographic
community right now and several are moving toward standardization. The
upshot is, by the time quantum computers are powerful enough to break
our current cryptography we should already be switched over to new
algorithms that are not vulnerable.

## <u>What will matter <i>then</i> already matters <i>now</i></u>

Because security experts and cryptographers are already working on
replacement algorithms, it is highly likely that the new algorithms will
already be available before quantum computers mature. ***So, there's
nothing to worry about, right***?

Well, that depends.

If you encrypt data now (for example, have a secure connection with your
bank), then someone could record your encrypted connection, and then
when they have a mature quantum computer, go back and decrypt it
(perhaps 10 or 15 years in the future). However, that's not the biggest
problem.

The biggest problem is, even if the new algorithms are available, ***how
many systems will they be installed on?*** Users already resist updating
their computers. In fact, the Equifax hack in 2017 happened, in part,
because of an unpatched server. ***New algorithms will do you no good if
you do not patch and update your systems***.

Another big problem is that many of our defenses are based on passwords.
Even many of our cryptographic keys are derived from or protected by
passwords in one form or another. ***Doubling the size of symmetric keys
will not solve the password problem***. In many applications,
post-quantum crypto will only be as strong as the (probably bad)
password protecting its keys.

And, of course, social engineering bypasses all cryptographic defenses
regardless of the algorithm. If our systems are being compromised by
phishing emails now, they will continue to be compromised in the
post-quantum world. ***Quantum-resistant certificates and signatures
can't stop a user from giving their login data to a scammer or scam
website***.

The point we are making here is that for the vast majority of users,
don't waste your time worrying about quantum computing and what it will
do to your systems. Take some time to figure out improved systems
security ***right now***! Quantum computing isn't going to matter for
many more years yet. And by the time it does, if you have been
developing good security deployments and operations, you may not even
notice when the switch-over happens. Instead, much like the Y2K bug,
you'll be more aware of the news reports about it than actually
experience any significant problems.

Still, if you have gotten this far, and read this entire article, and
still have questions, please reach out. We will be happy to answer them!

---

[^1]: 1984 American supernatural comedy film \"Ghostbusters.\" What
    percentage of the readers of this article will know this quotation?
    Is this footnote breaking the fourth wall?

[^2]: More typically, two keys, one to encrypt client-to-server traffic,
    and one to encrypt server-to-client traffic

[^3]: Technically, there is a bit more happening here to provide the
    authentication, but that is left out for simplicity.

[^4]: Many modern systems use a variant called Elliptic Curve Diffie
    Hellman, or ECDH.

[^5]: Named for Peter Shor.

[^6]: Named for Lov Grover.
 -->
