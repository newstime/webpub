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
