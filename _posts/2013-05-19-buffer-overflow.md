Classic Buffer Overflow
=======================

Description
-----------

See [CWE-120](http://cwe.mitre.org/data/definitions/120.html)

Historical Examples
-------------------
* OpenSSL's [CVE-2012-2110](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-2110) involved losing track of the buffer size. See the [fix](http://cvs.openssl.org/chngview?cn=22431)
* Samba's [CVE-2008-1105](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2008-1105) also involved miscalculation of the buffer size. See the [advisory](http://www.samba.org/samba/security/CVE-2008-1105.html) and [patch](https://bugzilla.redhat.com/attachment.cgi?id=305636&action=diff)

Mitigations
-----------
* Keep track of your array sizes. Check the size of your buffer as it is inputted. 
* In the case of C, use functions like strncpy() instead of strcpy().
* Avoid functions like gets that don't check the input size. 
 
Notes
-----

* Buffer overflows have been very common for a long time
* If you are clever enough, you can override the return pointer on the stack frame so that your own code is then executed. 
* Languages that enforce array lengths are not susceptible to this classic form (e.g. Java)
* Merely turning on the stack protector is not enough. We could easily craft an exploit that stays within the stack frame.

 

Running the Demo
----------------
```sh
  cd buffer-overflow
  make
```

