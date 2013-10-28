WebPub
=======

- Build by own crawer in ruby.
  - Would be cool to do this async

- Get an example sitemap.
- Sign a sitemap


### Creating a Self Signed Certificate

1. Create the private key. http://www.akadia.com/services/ssh_test_certificate.html

    $ openssl genrsa -des3 -out server.key 1024

Create a pass phrase when promoted. For examples included here, it is password.

2. Generate a CSR  http://www.akadia.com/services/ssh_test_certificate.html

    $ openssl req -new -key server.key -out server.csr

3. Remove Passphrase from Key http://www.akadia.com/services/ssh_test_certificate.html

    $ cp server.key server.key.org
    $ openssl rsa -in server.key.org -out server.key


4. Generating a Self-Signed Certificate http://www.akadia.com/services/ssh_test_certificate.html

    $ openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt

### Signing an XML Sitemap

    $ cp example_sitemap.xml example_sitemap.xml.org
    $ bin/sign_sitemap example_sitemap.xml.org cert.pem key.pem > example_sitemap.xml


### Get the public key as a pem from the cert file. http://stackoverflow.com/questions/17143606/how-to-save-public-key-from-a-certificate-in-pem-format

    $ openssl x509 -pubkey -noout -in cert.pem  > pubkey.pem

### Installing xmlsec

 http://www.aleksey.com/xmlsec/download.html


All steps are usual:

gunzip -c xmlsec1-xxx.tar.gz | tar xvf -
cd xmlsec1-xxxx
./configure --help
./configure [possible options]
make
make install
make check

Not sure why, but this all came in as xmlsec 1, that's fine though.

### Using xmlsec to sign

Add the signature transformation stuff to the file http://users.dcc.uchile.cl/~pcamacho/tutorial/web/xmlsec/xmlsec.html

Then, sign the file like this.

    $ xmlsec1 --sign --output signed.xml --privkey-pem key.pem example_sitemap.xml.org


Notice I'm using


### The public key is embeded, so simple call xmlsec1 to verify.


    $ xmlsec1 --verify signed.xml


Would be nice if I could compare the public key with a cert though, so I could
verify the entire cert chain.

I suppose, I could distribute the certificate myself, and just check against it.
No need to invovle certificates at all, those are only if I need to eastable
trust through a 3 party. The certifate is for deliverying a trusted public key.

### Using XMLSec to verify while passing the key

    $ xmlsec1 --verify --pubkey-pem pubkey.pem signed.xml

### Extracting the Public Key from a domain

So, we can request the key like this

openssl s_client -connect doximity.com:443 -showcerts

There is also no reason, I can go through verification of the certs my self, and
just requst the certificate as a pem resource, and then extract the public key
to use when verifying the xml file, and passing it in to override the embeedd
one. but it is nice to know the file hasn't been modified. Need to do full
verification though.

We can extract the key simple by pasteing any certifcate into the ascii armoured
BEGIN CERTIFICATE... stuff.

This will output a file, that can be passed to xmlsec.
