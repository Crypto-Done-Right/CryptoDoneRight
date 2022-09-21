---
layout: page
title: Certificates
type: concepts
update: Last Updated Sat, 8 Feb 2020 12:00:01 -0400
permalink: /articles/concepts/certificates.html
alerts:
  - id: 1
    type: danger
    description: "A vulnerability was found in the crypto library on Windows machines potentially causing forged certificates to be trusted (CVE-2020-0601). A patch was released from Microsoft in mid January, 2020."
    link: "https://nvd.nist.gov/vuln/detail/CVE-2020-0601"
  - id: 2
    type: warning
    description: "SHA1 certificates should not be deployed. Pre-image attacks have been demonstrated. Migrate certificates to use SHA-256 (SHA2-256) or greater."
    link: "https://eprint.iacr.org/2020/014.pdf"
further-reading:

related-articles:
- name: PKI
  description: "/articles/concepts/PKI/PKI.html"
warnings:

best_practices:
  - name: Use SHA-256 (SHA2-256) or stronger.
    description: "Certificates with some algorithms including SHA1 have been demonstrated to be vulnerable to pre-image attacks."
  - name: Don't trust (or deploy) self-signed certificates.
    description: "Self-signed certificates can be convenient during development and testing, but we should not trust self-signed certificates in the wild nor should we deploy self-signed certificates into the wild. We want to only deploy and trust certificates that have been verified by a trustworthy Certificate Authority (CA)."

---
Have you ever wondered why some websites show a lock next to them in your browser and some don't? You have probably heard that the lock means that it is safe to enter your credit card for example, or simply that it means you are browsing the web "securely". The determining factor of whether or not a lock gets displayed is the **certificate**. If the **certificate** is trustworthy, then your browser is able to set up an encrypted connection to the website and you are good to go. If the certificate cannot be verified, that's when you will see a warning.

There are two separate parts here, and we will address them both.

##### Keep in mind, you might also see **certificates** called **digital certificates**, **public key certificates**, or **X509 certificates**. These are all referring to the same thing, and we will just simply use **certificate**

#### First, what **is** a certificate?
A _certificate_ contains the public key of the party who the certificate belongs to, identifying information about the public key owner, and a [signature](/articles/concepts/asymmetric_cryptography.html) from whoever verified that this particular public belongs to this particular owner. The signing party is called the certificate **issuer**. Every certificate is, by definition, a stamp of approval for a public key, saying that it can be trusted. Therefore, every certificate is signed.

#### How do we decide to trust a certificate?
If the certificate issuer is trusted, we assume the public key and metadata contained in the certificate is itself trusted, too. What if we don't know and trust the certificate issuer? Then we check to see if the certificate we have sent along its chain. A **certificate chain** is simply the set of certificates we find when we start at the target certificate (i.e. example.com), look at the **issuer**'s certificate, look at the issuer's issuer's certificate, and so on until we arrive at the root. **Root certificates** are the end of the certificate chain. In a browser, root certificates are typically from well-known **Certificate Authorities**, such as Comodo or DigiCert. These companies are known and trusted around the internet, so their root certificates are installed, or **pre-trusted**, in the browser. If the root of a certificate chain is not from a trusted source, then we don't trust the target certificate either.

<p style="margin-bottom:0">Source: DigiCert blog at <a href="https://knowledge.digicert.com/solution/SO16297.html">https://knowledge.digicert.com/solution/SO16297.html</a></p>
<img style="margin-top:0" src="/img/certs/cert_chain.png"/>

#### How does a certificate contribute to encrypted internet communications?
Recall that one of the main items contained within a certificate is the owner's public key. Also recall that when we browse the internet, we should be doing so via the [TLS protocol](/articles/cryptographic_protocols/tls_1_3/tls_1_3.html). The premise of TLS is to provide **secure** connections between you and a web server. As part of the secure session establishment in TLS, the client will use the server's public key to encrypt what's called a _pre-master secret_ (remember that when something is encrypted with a public key, it can only be decrypted with the corresponding private key). You can read more about that on the TLS page, but in short it provides the information needed for both the client and the server to derive a symmetric encryption key that they will use to encrypt the rest of their session.

<div class="row">
  <div class="row">
    <div class="col-md-3 cert-img"><img src="/img/certs/cert-1.png"/></div>
    <div class="col-md-3 cert-img"><img src="/img/certs/cert-2.png"/></div>
    <div class="col-md-3 cert-img"><img src="/img/certs/cert-3.png"/></div>
    <div class="col-md-3 cert-img"><img src="/img/certs/cert-4.png"/></div>
  </div>
  <div class="row">
    <div class="col-md-3 cert-img"><img src="/img/certs/cert-5.png"/></div>
    <div class="col-md-3 cert-img"><img src="/img/certs/cert-6.png"/></div>
    <div class="col-md-3 cert-img"><img src="/img/certs/cert-7.png"/></div>
    <div class="col-md-3 cert-img"><img src="/img/certs/cert-8.png"/></div>
  </div>
</div>
