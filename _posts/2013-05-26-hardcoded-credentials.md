---
layout: catalog
---
Hard-Coded Credentials
======================

Description
-----------

See [CWE-798](http://cwe.mitre.org/data/definitions/798.html)

Historical Examples
-------------------
* The pyFTPD project in [CVE-2073](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2010-2073) had this issue, and fixed it by improving their installer (see [bug](http://bugs.debian.org/cgi-bin/bugreport.cgi?bug=585776))

Mitigations
-----------

* Extract your credentials out to a properties file, then install your system with the proper permissions on that properties file.
* Corollary: don't include default passwords anyway, make the user define them upon installation

Notes
-----

* Believe it or not, this is another common problem. Developers commonly misconceive that  you can keep secrets in your source code.
* The same kind of concept applies to encryption keys or pseudo-random number generator seeds - these are secrets that need to be treated as such.
* Obfuscation isn't the answer because reverse engineering is easier than you think. (Takes time and some skill, which crowds have).
* License keys have had this problem. Many companies today resort to a remote authentication for license products. But even then, it's still a tough problem today for desktop client applications (e.g. Windows Genuine Advantage).
* Hard-coding credentials also breaks maintainability and deployability. What if your database password was guessed, and you had to change it immediately?

Running the Demo
----------------
{% include demo_default.md %}

