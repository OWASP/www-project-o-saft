---
title: faqs
displaytext: FAQs
layout: null
tab: true
order: 1
---

* Where can I get missing Perl-Modules?<br>This depends on your OS and Perl installation, but just try ''cpan <Module-Name>'', e.g. ''cpan Net:DNS''
  * I am connected to the internet via a Proxy<br>open the cpan-shell using 'cpan' and configure your proxy settings: 'o conf init /proxy/' 
  * I can not download the requested files (the proxy needs authentication)<br>run 'cpan <Module-Name>' several times, read the error messages and copy the requested files manually to the paths (without any additional temporary extension of the name),<br>e.g. <nowiki>http://www.cpan.org/authors/01mailrc.txt.gz</nowiki> => <Your Program Path>/cpan/sources/authors/01mailrc.txt.gz

* I get the Error "invalid SSL_version specified at .../perl/vendor/lib/IO/Socket/SSL.pm line ..."
  * add options "--notlsv13 --nodtlsv1", e.g. "perl o-saft.pl +info your.tld --notlsv13 --nodtlsv1"
  * use ''+cipherall'' to check the ciphers for all protocols

* My local SSL libraries do *not* support legacy Protocols like SSLv2, SSLv3 or legacy Ciphers
  * use "o-saft.pl" for all protocols that are supported by your local computer
  * use "o-saft.pl +cipherall" (or "checkAllCiphers.pl") to get the ciphers for the missing protocols, or recompile 'Net::SSLeay' and/or ''openssl'' to support more protocols and ciphers, see (Documentation INSTALLATION)[O-Saft/Documentation#INSTALLATION] for details

* I can not use the latest features of the test (experimental) version
  * Please verify that you downloaded and unpacked the ('master.zip'-Archive)[https://github.com/OWASP/O-Saft/archive/master.zip]
  * some new functions are protected by the option "--experimental", please add it to your command (and take care what happens)

* o-saft.pl seems to hang
  * try one or all of following options (see (Documentation Performance Problems)[O-Saft/Documentation#Performance_Problems])<br>"--no-dns", "--no-http", "--no-cert", "--no-sni", "--no-openssl"