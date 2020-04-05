### LibreOffice zipped, compressed using brotli and archived using tar. Works with [aws-lambda-libreoffice](https://github.com/shelfio/aws-lambda-libreoffice).
##### Using layers provided here instead of the ones provided in [libreoffice-lambda-layer](https://github.com/shelfio/libreoffice-lambda-layer):
#####Pros:
* 6.4.0.3 Is provided with several files that fix a bug when [converting doc/docx files containing tables of contents](https://github.com/vladgolubev/serverless-libreoffice/issues/32)
* 6.4.2.2 Is just a newer version of LibreOffice containing different types of bugfixes, some that were necessary in my personal use cases
#####Cons:
* 6.4.0.3 Has a bigger size than [shelfio-layer](https://github.com/shelfio/libreoffice-lambda-layer/blob/master/layer.tar.br.zip) by 35MB when unpacked
    * Not really a con unless you want to use additional layers in your Lambda function
* 6.4.2.2 Has a bigger size than [shelfio-layer](https://github.com/shelfio/libreoffice-lambda-layer/blob/master/layer.tar.br.zip) by 50MB when unpacked 
    * Not really a con unless you want to use additional layers in your Lambda function
    * Reason behind bigger size difference is x86_64 libraries added to the package, because this version of LibreOffice was not compiled specifically for this use case, instead it is simple rpm installation of the package, and it was missing these libraries in Amazon Linux 2:
        * dbus-glib
        * cairo
        * cups
* 6.4.2.2 Might be a bit slower on cold starts (~16 seconds instead of ~15 seconds for my specific personal usage)