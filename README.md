### LibreOffice zipped, compressed using brotli and archived using tar. Works with [aws-lambda-libreoffice](https://github.com/shelfio/aws-lambda-libreoffice).
##### Using layers provided here instead of the ones provided in [libreoffice-lambda-layer](https://github.com/shelfio/libreoffice-lambda-layer):
##### Pros:
* 6.4.0.3 Is provided with several files that fix a bug when [converting doc/docx files containing tables of contents](https://github.com/vladgolubev/serverless-libreoffice/issues/32)
* 6.4.2.2 Is just a newer version of LibreOffice containing different types of bugfixes, some that were necessary in my personal use cases
##### Cons:
* Both versions have a bigger size than [shelfio-layer](https://github.com/shelfio/libreoffice-lambda-layer/blob/master/layer.tar.br.zip) by ~35MB when unpacked
    * Not really a con unless you want to use additional layers in your Lambda function and lack free space.
    * Reason behind bigger size in 6.4.0.3 are extra share/config folders added from rpm LibreOffice installation to [shelfio-layer](https://github.com/shelfio/libreoffice-lambda-layer/blob/master/layer.tar.br.zip), in order to fix a [bug](https://github.com/vladgolubev/serverless-libreoffice/issues/32)
        * Definitely not all contents from the share/config directory are actually necessary for fixing the bug, but since it's an older version of Libre, I didn't bother to look for the actually necessary contents
    * Reason behind bigger size in 6.4.2.2. version difference is x86_64 libraries added to the package, because this version of LibreOffice was not compiled specifically for this use case, instead it is simple rpm installation of the package, and it was missing these libraries in Amazon Linux 2:
        * dbus-glib
        * cairo
        * cups
        * libXinerama
