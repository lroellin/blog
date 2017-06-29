+++
title = "SSL Certificate How-To (Apache/OpenSSL)"
date = 2014-08-14T04:28:47+02:00
+++

Note: please keep in mind that this was written in 2014. The process is still the same, although I now prefer a setup with nginx and Let's Encrypt. This is just here to understand how this whole thing works, and how to possibly set it up. The algorithms and key lengths may not be recommended anymore.

This how-to describes how to enable/change SSL certificates and how to generate the CSR you need. This follows to my environment, as it is more or less a documentation.
# Terms and concepts
First, I'll explain to you what all the terms you'll meet mean.
## Private/public key
I don't want to go into any depths on how this works mathematically, but I'll tell you what you need to know as a system administrator.

* Your private key belongs only on the server (and stays there) that needs it for encryption/decryption
* Your public key also belongs on that server, but the server sends it on the start of any SSL session
* Your private key is needed to encrypt/decrypt data that is decrypted/encrypted via the public key
* Your public key is derived from your private key, therefore anyone with your public key can prove your identity
* **If your private key gets stolen, your SSL encryption is worthless**

## CA - Certificate Authority
A certificate authority is an institution that signs your SSL certificate - it signs your public key. Why do we need this?

A CA proves that this domain is yours and you don't register certificates for www.google.com. If browser developers decide that they trust this CA in the approval process, it gets added to the trust store. If your SSL certificate is signed by any trusted CA, your SSL certificate is trusted too.
## CSR - Certificate Signing Request
A CSR is a request to get your certificate signed by a CA. You generate a CSR by using your private key and send this to the CA. If they've approved your request, they'll sign your CSR with their own CA private key. This generates your SSL certificate.

Therefore, anybody with your new SSL certificate can prove two things:

* It is signed by you (you used the private key for the CSR)
* It is signed by a CA (they used their private key)

## Certificate Chain
Now, I said that they sign it with their private key. However, they won't sign it with their "master-key" (technically: Root CA). This has two reasons:

* If the master-key gets involved in signing, it may get stolen
* If it gets stolen, the *whole* CA is trust-less and therefore worthless

They however use sub-CAs to sign your certificate. This also means that it's possible for sub-departments to do this, without the risk of the master-key being everywhere.

As I said, browsers trust the CA. But your certificate is not signed directly by this CA. This means, you not only have to send your certificate and the CA's, but every certificate in between. This is called the certificate chain. In my example, this is

* Root CA Certificate - AddTrustExternalCARoot.crt - **this is trusted by any browser**
  * Intermediate CA Certificate - COMODORSAAddTrustCA.crt
  * Intermediate CA Certificate - COMODORSADomainValidationSecureServerCA.crt
     * Your SSL Certificate - www_dreami_ch.crt - **this is your certificate**

These two certificates are needed to form a "bridge" between your certificate and the CA certificate

You need to send browsers the whole chain of certificates. You usually get these along with your SSL certificate.
# Setup
First, you'll need to generate your private key and a CSR, signed with it. To do this, switch to a place to store all these files. For me, this is

```bash
cd /etc/ssl/2014
```

On Linux with OpenSSL, generation can be done in one command:

```bash
openssl req -nodes -newkey rsa:2048 -keyout private.key -out server.csr
```

I recommend 2048 for key length. It's the length (in bits) of your private key. As said, I won't get into any of these, but let's say it's a fine trade-off between two things that need attention in encryption

* Longer: key is stronger to crack
* Shorter: encryption/decryption is faster

You'll need to give two file names.

* `-keyout` parameter: where to store the private key
* `-out` parameter: where to store the CSR (signed with your private key)


You'll then be asked several things. Here are my answers:

    Country Name (2 letter code) [AU]: CH
    State or Province Name (full name) [Some-State]: Schwyz
    Locality Name (eg, city) []: Tuggen
    Organization Name (eg, company) [Internet Widgits Pty Ltd]: Dreami
    Organizational Unit Name (eg, section) []: (blank)
    Common Name (eg, YOUR name) []: www.dreami.ch
    Email Address []: postmaster@dreami.ch
    A challenge password []: (blank)
    An optional company name []: (blank)[/code]

Then, provide the CSR to your CA:

```bash
# cat server.csr
 -----BEGIN CERTIFICATE REQUEST-----
 MIICwjCCAaoCAQAwfTELMAkGA1UEBhMCQ0gxDzANBgNVBAgMBlNjaHd5ejEPMA0G
(shortened)
 d2FcGG6zpUx14qh1wbh6zAdEkOIquxLgewjArfac8pgKh2kF8N4=
 -----END CERTIFICATE REQUEST-----
 ```

They will test several things and, after some time, send your certificate, possibly along with all the Intermediate and Root certificates.

You can then bundle all CA certificates (Root and Intermediate), so you only have two files afterwards:

* Bundle
* Your certificate

To bundle these, you have to paste them one-after-another into a text file. The order is important. It's reverse of the certificate tree.

* Intermediate CA Certificate - COMODORSADomainValidationSecureServerCA.crt
* Intermediate CA Certificate - COMODORSAAddTrustCA.crt
* Root CA Certificate - AddTrustExternalCARoot.crt

```bash
cat COMODORSADomainValidationSecureServerCA.crt COMODORSAAddTrustCA.crt AddTrustExternalCARoot.crt > www_dreami_ch.ca-bundle
```

The filename is up to you.

Then, you have to add these to your virtual host. **You have to make a separate virtual host from your already existing HTTP one.** I did this even in a separate file, so I have two files now:

/etc/apache2/sites-available/dreami.ch (link to sites-enabled/)
/etc/apache2/sites-available/ssl-dreami.ch (link to sites-enabled/)

This way I can clearly differentiate. For example, since this blog is not HTTPS protected, it only exists in "dreami.ch" but not in "ssl-dreami.ch"

So, edit your virtual host entry:

    <VirtualHost *:443>
        DocumentRoot [removed, identical to other virtual host]
        ServerName <a href="http://www.dreami.ch">www.dreami.ch</a>
        SSLEngine On
         # Private Key
        SSLCertificateKeyFile /etc/apache2/ssl/2014/private.key
         # Public Key/Certificate
         SSLCertificateFile /etc/apache2/ssl/2014/www_dreami_ch.crt
         # CA Chain
        SSLCertificateChainFile /etc/apache2/ssl/2014/www_dreami_ch.ca-bundle

        # Other directives here

Then save that file and restart Apache

```bash
/etc/init.d/apache2 restart
```

# Tools
The most important tool is <a href="https://www.ssllabs.com/ssltest/">Qualys's SSL Labs</a>. It tells you if everything works and what you can improve on.