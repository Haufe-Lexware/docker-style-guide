Prerequisites
=============

Use only certs that directly fit to the desired host/domain/ip, don't use sth. like "cname" entries for DNS because docker will notice and reject the repository.

**BEWARE!!**
--------------------

When using a server (SSL) certificate with "Intermediate CA" on/with nginx,
you MUST create a file that contains "all(?)" certificates and use THAT!

Example
-------

Create a private key

    openssl genrsa -out dockerhub.haufe-lexware.com.key 2048

Generate a certificate signing request (CSR)

    openssl req -new -key dockerhub.haufe-lexware.com.key \
      -out dockerhub.haufe-lexware.com.csr

Send the request to the "authority" (Hi Steffen!!) that provides you with the
signed certificate

    $ ls -1
    dockerhub.haufe-lexware.com_150508.cert
    dockerhub.haufe-lexware.com.csr
    dockerhub.haufe-lexware.com.key
    IntermediateCA.CERT

If you get some additional certificate (here:IntermediateCA), then you have to create a "bundle" to be used as the certificate in nginx.

    cat dockerhub.haufe-lexware.com_150508.cert IntermediateCA.CERT \
      >> bundle.crt

Notes
-----

To check the contents of a certificate, start openssl
in "interactive mode" and paste the certs content to the commandline

    openssl x509 -text -noout

---

