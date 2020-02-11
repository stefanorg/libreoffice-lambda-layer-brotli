libreoffice zipped & compressed using brotli, taken from https://github.com/shelfio/libreoffice-lambda-layer.
directories from the original libreoffice 6.4.0.3 were added to the archive:
* share/config/soffice.cfg
* share/config/webcast
* share/config/wizard

these directories added ~35mb to the final layer, but fixed the bug when doc/docx files containing tables of contents could not be converted to pdf (https://github.com/vladgolubev/serverless-libreoffice/issues/32)
