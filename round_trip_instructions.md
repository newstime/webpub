Round Trip Instructions
=========================


The round-trip instructioins take you through a tour of the system.

We will assume you have already render your site, or otherwise dumped the html
content. You can do this with spydering software, or a static site generation
tool. You can also accomplish this by creating the html by hand. You will want
to ensure that all files linked to have been dumped, so that there are no
deadlink, or obmittions in the publication. It is also, possible not good
pratice to included files in the manifest, that aren't linked to from the root
somehow.

I don't this that will be a requirement though, just a though. I think it is
more free and open ended, and praticale, if they don't have to be linked. The
will be include.

(All command executed from root of publication)

## 1. Create the Manifest

    $ ../bin/create_manifest https://theindependent.com/2013/10/24

webpub.manifest file is produced.

## 2. Sign the Manifest

Pass private key in for signing. For more information on keys, see createing
private keys.

    $ ../bin/sign_manifest ../credentials/key.pem

webpub.signature file is produced.

## 3. Verify the Manifest

Pass cert in for verifcation. See, creating cert for more information on cert.

    $ ../bin/verify_manifest ../credentials/cert.pem
    OK

## 4. Verify the Content

Finally, verify the signature of every item of content, to ensure it matches the
sha1.

    $ ../bin/verify_content
    OK  assets/angular.js?body=1
    OK  assets/application.css?body=1.css
    OK  assets/application.css?body=1orig
    OK  assets/application.js?body=1
    OK  assets/articles/curiosity_rover2.j
    ...

Now you know you are reading the news, and who it's from. They can't change it,
and you have proof they wrote it. Very powerful.
