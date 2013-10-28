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
