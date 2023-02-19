---
layout: page
title: SHA1
type: hashing_algorithms
update: Last Updated Thu, 12 Dec 2018 12:00:01 -0400
permalink: /articles/hashing_algorithms/sha1.html
alerts:
  - id: 1
    type: danger
    description: "Warning: This technology is obsolete!"
  - id: 2
    type: recommended
    description: "Migration plan: moving from SHA-1 to SHA-2."
    link: /articles/hashing_algorithms/sha1/sha1_migration
  - id: 3
    type: warning
    description: Click to judge how much time do you have for migration.
    link: /articles/hashing_algorithms/sha1/sha1_it_quickstart.html
further-reading:
  - name: History of Hash Functions
    link: https://www.esat.kuleuven.be/cosic/publications/article-1532.pdf
  - name: Comparative Study Between MD5 and SHA-1
    link: http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.659.1400&rep=rep1&type=pdf
  - name: Comparisons between the different SHAs
    link: https://en.wikipedia.org/wiki/Secure_Hash_Algorithms

---
SHA-1 is the first version in the Secure Hash Algorithm (SHA) family that was made widely popular. Usage of this algorithm with an input value provides a 160 bit hexadecimal value with hash properties (cannot be reversed to find the original value ). This method is used to maintain integrity of data as different input values always create different hash values and therefore making a duplication of hash difficult. SHA-1 was an improvement over a previous hashing algorithm called MD5.
