---
layout: FAQ
title: FAQ
type: TLS 1.2
upper-link: /articles/cryptographic_protocols/tls_1_2/tls_1_2.html
---
<p>
  <img src="/img/common/faqs.jpg" style="width:500px;height:100px;" class="center" />
  <center><h2>TLS/TLSv1.2 FAQs</h2></center><br /><br />
  <blockquote>
		<ul>
			<a href="#whattls?"><li>What exactly is TLS anyway?</li></a>
			<a href="#istlsrequired?"><li>Why Is TLS 1.2 necessary?</li></a>
			<a href="#consequencesoftls"><li>What are the consequences if I don’t upgrade to TLS 1.2?</li></a>
			<a href="#tlsv1.2vulnerable"><li>How can I tell if my site is vulnerable?</li></a>
			<a href="#updatedsslcert"><li>
			I updated our SSL certificate. Isn’t that good enough?
			</li></a>
			<a href="#complianttlsv1.2"><li>What do I need to do to ensure that my site is compliant?</li></a>
			<a href="#tlsv1.2browser"><li>What browsers/versions will provide the option for TLS 1.2?</li></a>
			<a href="#librariestlsv1.2"><li>Whare are some popular libraries to implement TLSv1.2?</li></a>
			<a href="#performancetlsv1.2"><li>Why TLSv1.2 when TLSv1.3 is already out?</li></a>
			<a href="#recommendedciphers"><li>What are the recommended ciphers for use with TLSv1.2?</li></a>
		</ul>
  </blockquote><br /><br />
	<p id="whattls?">
		<li><strong>What exactly is TLS anyway?</strong><br /><br />
		TLS stands for “Transport Layer Security.” It is the security protocol that allows computers to communicate over the internet securely, without the transmissions being vulnerable to anyone they aren’t intended for. Without TLS, you wouldn’t be able to use your credit card on eCommerce sites or log into your bank account online.</li><br /><br />
	</p>
	<p id="istlsrequired?">
		<li><strong>Why Is TLS 1.2 necessary? </strong><br /> <br />
		Due to several weaknesses found in TLS 1.0, many websites and internet services are now starting to require the use of TLS1.2.  The latest PCI compliance standards require that any site accepting credit card payments use TLS 1.2 after June 30th, 2018*.  Even though you have some time before it is required for PCI compliance, several internet services are moving to require the support of TLS 1.2 as early as next year.  Services such as PayPal, Authorize.net, Stripe, UPS, FedEx and many others already support TLS 1.2 and have indicated that they will eventually refuse TLS 1.0 connections.  The dates for when they will refuse TLS 1.0 connections are not clear, but your safest action is to upgrade to TLS 1.2 sooner than later.</li><br /><br />
	</p>
	<p id="consequencesoftls">
		<li><strong> What are the consequences if I don’t upgrade to TLS 1.2? </strong><br /><br />
		First and foremost, your customer’s data is at risk.  In the event of a data breach, consequences for not being PCI compliant can include fines and your merchant bank can terminate your ability to process credit cards. <br /> <br />
		Second, crucial functions on your website will stop working overtime as the services your website uses require TLS 1.2.  This means that your payment processing and real-time shipping rates could stop working at some point over the next year if you don’t address it. </li><br /><br />
	</p>
	<p id="tlsv1.2vulnerable">
		<li><strong> How can I tell if my site is vulnerable? </strong><br /><br />
		The easiest and one of the simplest way to test the security of your site or web server is to run your website through the online ssl tester. The link for this SSL web server tester is <a href="https://www.ssllabs.com/ssltest/"> here </a>.
		SSL Labs by Qualys is a collection of documents, tools and thoughts related to SSL. It's an attempt to better understand how SSL is deployed, and an attempt to make it better.</li><br /><br />
	</p>
	<p id="updatedsslcert">
		<li><strong>I updated our SSL certificate. Isn’t that good enough?</li></strong><br /><br />
		No. To put it simply, your SSL certificate  is literally step 1 of "50" to ensure that your webserver is hardened. There are a lot of configuration that needs to be done on your server to ensure that all aspects of server is closed to any sort of attacks. I would suggest also revisiting the page about "PIC" model to get a feel of what I am aiming at over here.<br /><br />
		There are multiple configurations in most web servers which are weak by default. They use weak protocols such as SSLv2 or SSLv3. They support broken cipher suites such as RC4 etc. Security features such as HSTS, OCSP stapling are disabled by default.<br /><br />
		In short, carefully vetting each and every aspect of configuration must be done meticulously to ensure that there are no holes that a potential adversary can use as an advantage to squirm their way into the server.</li><br /><br />
	</p>
	<p id="complianttlsv1.2">
		<li><strong> What do I need to do to ensure that my site is compliant? </strong><br /><br />
		Unfortunately, this is not a simple answer. There are several variables and a number of systems and software platforms involved. Every business has a different configuration, and there is no easy set of step-by-step instructions that will work in all cases.<br /><br />
		Below is a simple example:
		At a high level, you will need to ensure that the following platforms and connections are compatible with TLS 1.2: <br /><br />
			<ul>
				<li>Web Server</li>
				<li>Internet Information Services (IIS)</li>
				<li>.NET Framework</li>
				<li> Maybe some eCommerce Application</li>
			</ul><br />
		You may also need to look at the compatibility of the browsers you support for your users as well as any web services involved in your payment and fulfillment process.<br />
		Another good practice is run your website through a bunch of tests in the SSL Labs site and ensure that your grade is A and above.</li><br /><br />
	</p>
	<p id="tlsv1.2browser">
		<li><strong>What browsers/versions will provide the option for TLS 1.2?</strong><br />
		These browser versions will support the option to use TLS 1.2, regardless of what operating system
		they  are  used  on.    Below  is  a  list  of  the  browsers  and  versions  that  are usually certified  for  use  on most third-party softwares and support TLS 1.2.<br /><br />
		Browser Versions <br />
		------------------------------------ <br />
		Internet Explorer 8, 9, 10 & 11  <br />
		Chrome 42, 43 & 44 <br />
		Firefox 34, 35 &36 <br />
		Safari 7 & 8 </li><br />
	</p>
	<p id="librariestlsv1.2">
		<li><strong>Whare are some popular libraries to implement TLSv1.2?</strong><br />
		<strong>Python:</strong><br />
		ssl library <br />
		pyopenssl library <br /><br />
		<strong>Java:</strong><br />
		If your application runs on Java 1.7 or Java 1.6 (update 111 or later), you can set the https.protocols system property when starting the JVM to enable additional protocols for connections made using the HttpsURLConnection class – for example, by setting -Dhttps.protocols=TLSv1.2.<br /><br />
		<strong>C++:</strong>
		Botan, PolarSSL, Mozilla NSS, Wolf and GnuTLS.<br />
		All except Botan are not C++ specific so they do not have nice C++ objects and resource management.</li><br /><br />
	</p>
	<p id="performancetlsv1.2">
		<li><strong>How much performance overhead does TLSv1.2 have?</strong><br >
		According to IETF document <a href="https://datatracker.ietf.org/doc/html/draft-mattsson-uta-tls-overhead-01">Overview and Analysis of Overhead Caused by TLS</a>, For everything but very short connections, TLS is not inducing any major traffic overhead (nor CPU or memory overhead). Server people from Google Gmail has stated that “TLS accounts for less than 1% of the CPU load, less than 10 KB of memory per connection and less than 2% of network overhead”. Main impact of TLS is increased latency, this can by reduced by using session resumption, cache information closer to end users, or waiting for TLS 1.3.</li><br /><br />
	</p>
	<!-- <p id="certificatestlsv1.2">
		<li><strong>What kind of certificates do I use with TLSv1.2?</strong><br />
		Read the following document: <a href="tls_1_2_best_practices.html"> Best practices to deploy certificates </a></li><br /><br />
	</p> 
	THIS IS COMMENTED OUT BECAUSE tls_1_2_best-practices.html does not exist 
	-->
	<p id="popularcatlsv1.2">
		<li><strong>Who are some of the most popular CAs available?</strong><br />
		GoDaddy, Symantec, Digicert are some of the well known CAs around. You could also consider options like <a href="https://letsencrypt.org/">Let'sencrypt </a>which are free and well-trusted.</li><br /><br />
	</p>
	<p id="tlsv1.3vstlsv1.2">
		<li><strong>Why TLSv1.2 when TLSv1.3 is already out?</strong><br />
		<strong>Simply for backware compatability.</strong> While TLSv1.3 does provide better configurational options in terms of improved versions of algorithms as well as improved performance, adoption of new protocols is slow and that might mean issues in interoperability. The safe option in this case where TLSv1.2 and TLSv1.3 are both equally safe protocols, is to run an environment which supports both the protocols.</li><br /><br />
	</p>
	<p id="recommendedciphers">
		<li><strong>What are the recommended ciphers for use with TLSv1.2?</strong><br />
		<strong>TLS Recommended Ciphers:</strong><br />
		TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256 as defined in RFC 5289 <br />
		TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384 as defined in RFC 5289 <br />
		TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256 as defined in RFC 5289 <br />
		TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384 as defined in RFC 5289 <br />
		TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 as defined in RFC 5289 <br />
		TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384 as defined in RFC 5289 <br />
		TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256 as defined in RFC 5289 <br />
		TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384 as defined in RFC 5289 <br /><br />
	<strong>Avoid the following ciphers: </strong><br />
		TLS_DHE_RSA_WITH_AES_128_CBC_SHA <br />
		TLS_DHE_RSA_WITH_AES_256_CBC_SHA <br />
		TLS_DHE_RSA_WITH_AES_128_CBC_ SHA256 <br />
		TLS_DHE_RSA_WITH_AES_256_CBC_ SHA256 <br /></li><br />
	</p>
</p>