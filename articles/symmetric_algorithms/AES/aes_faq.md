---
layout: FAQ
title: FAQ
type: AES
upper-link: /articles/symmetric_algorithms/aes/aes.html
---
<p>
<img src="/img/common/faqs.jpg" style="width:500px;height:100px;" class="center" />

            <center><h2>AES FAQs</h2></center>
            <br /> <br />
            <blockquote>
        			<ul>
        			<a href="#whataes"><li>
        			What is AES and why is it used?
        			</li></a>
        			<a href="#commonapplications"><li>
        			What are some common applications?
        			</li></a>
        			<a href="#useaes"><li>
        			How will I use AES?
        			</li></a>
        			<a href="#aesmodesofoperation"><li>
        			What are "Modes of Operation" and why are they important?
        			</li></a>
        			<a href="#aeskeysizes"><li>
        			Why are there different key sizes?
        			</li></a>
        			<a href="#aesattacks"><li>
        			What kind of attacks are possible on AES?
        			</li></a>
        			<a href="#aesadvantages"><li>
        			Advantages of using AES over other encryption algorithms?
        			</li></a>
        			</ul>
              </blockquote>
		 <br /> <br />
			<p id="whataes">
            <strong>What is AES and why is it used?</strong> <br /> <br />

            The Advanced Encryption Standard, or AES, is a symmetric block cipher<link to block cipher> encryption algorithm.There are a number of encryption packages available which leverage AES, and it is the first open and publicly approved cipher by the U.S. NSA (National Security Agency) for use with top secret information when employed in a NSA-approved cryptographic module.    <br /> <br />

            <strong>What are the features/capabilties of AES?</strong><br /> <br />

           The selection process for this new symmetric key algorithm was fully open to public scrutiny and comment; this ensured a thorough, transparent analysis of the designs submitted.

			NIST specified the new advanced encryption standard algorithm must be a block cipher capable of handling 128 bit blocks, using keys sized at 128, 192, and 256 bits; other criteria for being chosen as the next advanced encryption standard algorithm included: <br /><br />

			<strong>Security:</strong> Competing algorithms were to be judged on their ability to resist attack, as compared to other submitted ciphers, though security strength was to be considered the most important factor in the competition.<br />
			<strong>Cost:</strong> Intended to be released under a global, nonexclusive and royalty-free basis, the candidate algorithms were to be evaluated on computational and memory efficiency. <br />
			<strong>Implementation:</strong> Algorithm and implementation characteristics to be evaluated included the flexibility of the algorithm; suitability of the algorithm to be implemented in hardware or software; and overall, relative simplicity of implementation. <br /> <br />

			A good read: <a href="https://searchsecurity.techtarget.com/definition/Advanced-Encryption-Standard">Learn more about AES</a> <br /><br />
			</p>
			<p id="commonapplications">
            <strong>What are some common applications?</strong><br /> <br />

			AES is a symmetric key algorithm (translates to the the two parties communicating sharing the same keys for encryption and decryption) and can be used anywhere encryption is needed for example to secure communication between two parties or to encrypt file systems at rest.

			There is no particular list of applications of AES, but many banking systems for example, use AES. You'll see a lot of websites running https:// use AES.<br /> <br />
			</p>
			<p id="useaes">
            <strong>How will I use AES?</strong><br /> <br />

            Firstly, never roll out your own crypto. Implementing AES in software for example can introduce a lot of bugs that will effictively make AES useless.

			For software developers, there are multiple libraries in a lot of popular programming languages that are well reputed and current. For IT professionals, vendors usually ship AES with the product you are buying, always watch out for the feature specifications and ensure that latest key sizes (AS of 2018: 128 bit, 256 bit) are supported.  <br /> <br />
			</p>
			<p id="aesmodesofoperation">
            <strong>What are "Modes of Operation" and why are they important?</strong><br /> <br />

            Block ciphers should not be used as described in their original definitions. This is inherently weak since an adversary can build up a dictionary of different plain texts and their corresponding ciphertexts and use them to decipher an encrypted message. Besides the weakness in using encryption algorithms directly, there is also an added limitation where direct use cannot work on variable length of messages (the length of a message should be a multiple of the cipher block size in length).<br /><br />

			The two popular modes of Operations are: <br /><br />
			<ul>
			<li>Cipher Block Chaining (CBC) </li>
			<li>Counter (CTR) </li></ul>	 <br /> <br />
			</p>
			<p id="aeskeysizes">
            <strong>Why are there different key sizes? </strong><br /> <br />

            All the encryption algorithms can operate in different key sizes. A cipher is no stronger than its key length: if there are too few keys, an attacker can enumerate all possible keys. These different key sizes have different impacts on hardware/software and therefore an ideal sweet spot is choosing the right key length that offers enough security and provides good performance. Usually, the longer the key size the better the security but there are possible exceptions (for example, AES). <br /><br />

			The length of each of the Block (broken chunks of data) is 128 bits and the available key length are 128, 192 or 256 bits.  <br /> <br />
			</p>
			<p id="aesattacks">

            <strong>What kind of attacks are possible on AES?</strong><br /> <br />

            AES is a safe protocol to use. There have been no practical attacks demonstrated against AES. That does not however mean that <a href="https://www.schneier.com/blog/archives/2011/08/new_attack_on_a_1.html">no attacks have been discovered.</a><br /> <br />

            Ultimately, updating to the latest security protocols protects you, your users, and your reputation.  <br /> <br />
			</p>
			<p id="aesadvantages">
            <strong> Advantages of using AES over other encryption algorithms?  </strong><br />
            As of 2018, there haven't been any practical attacks that have broken AES 128bit or AES 256bit keys. This places AES as one of the best encryption algorithms to deploy. Although it can debated that there are better algorithms, AES is popular, well accepted and widely deployed on the internet! This makes this one of the widely well researched and maintained protocols.

			Click <a href="https://techdifferences.com/difference-between-des-and-aes.html">here</a> for understanding some of the high level differences between DES and AES:  <br /> <br />
			</p>
			<p id="aesperformance">
            <strong> How much overhead does it introduce in software and hardware? </strong><br />
            AES is a well known computationally and memory effective. Modern CPUs even have specific opcodes to speed up AES computation.
			Utilizing AES should not prove to be of any burden to an average computer. AES libraries have been developed for Raspberry Pis as well:<a href="http://spaniakos.github.io/AES/"> <http://spaniakos.github.io/AES/> </a>
			</p>

      <p id="sslconfig">
            <strong> How do I configure my server such that they use AES? </strong><br />
            AES in itself is not sufficient to be used for anything in particular since it is a symmetric key encryption. All symmetric key encryptions are weak to the key distribution problem. So, AES is used in conjuction with other crpytopgraphic primitives which is called a CipherSuite. Most server's are configured with these CipherSuites. Below are a few examples of how to configure with these CipherSuites:

            <blockquote>
              <strong>Apache</strong> <br />
              SSLCipherSuite ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:RSA+AESGCM:RSA+AES:!aNULL:!MD5:!DSS
              <br /><br />
              <strong>NGINX</strong> <br />
              ssl_ciphers ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:RSA+AESGCM:RSA+AES:!aNULL:!MD5:!DSS;
            </blockquote>
      </p>
        <button onclick="topFunction()" id="myBtn" title="Go to top">Top</button>
        <script type="text/javascript">
                      // When the user scrolls down 20px from the top of the document, show the button
            window.onscroll = function() {scrollFunction()};
            function scrollFunction() {
                if (document.body.scrollTop > 20 || document.documentElement.scrollTop > 20) {
                    document.getElementById("myBtn").style.display = "block";
                } else {
                    document.getElementById("myBtn").style.display = "none";
                }
            }
            // When the user clicks on the button, scroll to the top of the document
            function topFunction() {
                document.body.scrollTop = 0; // For Safari
                document.documentElement.scrollTop = 0; // For Chrome, Firefox, IE and Opera
            }
        </script>
          </p>
