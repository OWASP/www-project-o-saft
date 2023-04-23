---

layout: col-sidebar
title: OWASP O-Saft
tags: tlsm, ssl, osaft
altfooter: true
level: 2
type: tool
auto-migrated: 0
pitch: O-Saft is an easy to use tool to show informations about SSL certificate and tests the SSL connection according given list of ciphers and various SSL configurations.

---

# O-Saft
**OWASP SSL advanced forensic tool / OWASP SSL audit for testers**

O-Saft is an easy to use tool to show informations about SSL certificate and tests the SSL connection according given list of ciphers and various SSL configurations.

It's designed to be used by penetration testers, security auditors or server administrators. The idea is to show the important informations or the special checks with a simple call of the tool. However, it provides a wide range of options so that it can be used for comprehensive and special checks by experienced people.

O-Saft is a command-line tool, so it can be used offline and in closed environments. There is also a GUI based on Tcl/Tk. However, it can simply be turned into an online CGI-tool (please read documentation first).

## Introduction 
### Quick Installation:
* Download and unpack o-saft.tgz (Stable Release)
* to run o-saft: Ensure that following perl modules (and their dependencies) are installed
  * IO::Socket::INET, IO::Socket::SSL, Net::SSLeay
  * Net::SSLinfo, Net::SSLhello (which are part of the tarball)
* read and (re-)move o-saft-README
* Show help
```
 o-saft --help=commands
 o-saft --help
```
* Start 
```
 o-saft +info  your.tld
 o-saft +check your.tld
 o-saft +quick your.tld
 o-saft +cipherall your.tld
 o-saft +cipherall --starttls=pop3 pop3.your.tld:110
 o-saft +info mail.tld:25 --starttls
```
* to run the optional **checkAllCiphers** (tiny program to check solely ciphers, like command '+cipherall'):<br>It usually does not need any perl module to be additionally installed
  * Socket (should be part of your perl installation)
  * Net::SSLhello (which is part of the tarball)
  * NET::DNS (only needed, if option '--mx' is used) 
* Start
```
 checkAllCiphers your.tld
 checkAllCiphers --starttls=pop3 pop3.your.tld:110
 checkAllCiphers --mx your.tld:25 --starttls=smtp
```
* Simple GUI
```
 o-saft.tcl
 o-saft.tcl your.tld
```

* Kali 2019
```
 apt install o-saft # installs version 19.01.19
 apt install libidn11-dev libidn2-0-dev libzip-dev libsctp-dev libkrb5-dev
 cd /usr/share/o-saft
 # get updated script
 curl -O contrib/install_openssl.sh https://raw.githubusercontent.com/OWASP/O-Saft/master/contrib/install_openssl.sh
 sh contrib/install_openssl.sh --m
 # enjoy commands as described before ...
```

## Description

The main idea is to have a tool which works on common platforms and can simply be automated.
### In a Nutshell:
* show SSL connection details
* show certificate details
* check for supported ciphers
* check for ciphers provided in your own libssl.so and libcrypt.so
* check for ciphers without any dependency to a library (+cipherall)
* checks the server's priority for ciphers (+cipherall) 
* check for special HTTP(S) support (like SNI, HSTS, certificate pinning, SSTP)
* check for vulnerabilities (BEAST, CRIME, DROWN, FREAK, Heartbleed, Lucky 13, POODLE, RC4 Bias, Sweet32 ...)
* check the length of Diffie Hellman Parameters by the cipher (+cipherall needs option '--experimental')
* may check for a single attribute
* may check multiple targets at once
* can be scripted (headless or as CGI)
* should work on any platform (just needs perl, openssl optional)
* can be used in CI / CD environments
* output format can be customized
* various trace and debug options to hunt unusual connection problems
* supports STARTTLS for various protocols 
  * SMTP, POP3, IMAP, LDAP, RDP, XMPP, IRC (experimental) ...
  * customize your own STARTTLS sequence using --starttls='CUSTOM', see help for '--starttls_phase1..5' and '--starttls_error1..3'
  * without using openssl
  * slows down to prevent blockades of requests due to too much connections (supported for some protocols like SMTP)
* Proxy is supported (besides commands using openssl)
* check of STARTTLS/SMTP for all servers of a MX Resource Record (e.g. checkAllCiphers --mx your.tld:25 --starttls=smtp)
* checkAllCiphers.pl and '+cipherall' support DTLS for '--experimental' use (if records are *not* fragmented)

## New Features of Test Version

### Quick Installation (latest version 23.04.23):
* Download and unpack master.zip from [github.com/OWASP/O-Saft](https://github.com/OWASP/O-Saft/) or use [o-saft.tgz](https://github.com/OWASP/O-Saft/raw/master/o-saft.tgz)
* Start INSTALL.sh (if you want)
* Enjoy new functionality:
  * '+cipherraw' and 'checkAllCiphers.pl' changed bahavior to check sni (now the default is to use solely sni >=tls1
     * new option --togglesni tests without and with sni in one call
  * checkAllCiphers.pl/+cipherall: shows the length of dh_parameter for ciphers with DHE and DH_anon, shows the elliptic curve that the server prefers for ECDHE (independant from openssl)
  * checkAllCiphers.pl/+cipherall: support of fagmented messages reassembling SSL/TLS-records
  * please give us feedback via github <!--- via the [https://lists.owasp.org/mailman/listinfo/o-saft mailinglist]  -->

