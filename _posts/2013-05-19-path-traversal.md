Path Traversal
==============

Description
-----------

See [CWE-22](http://cwe.mitre.org/data/definitions/22.html)

Mitigations
-----------

* Canonicalize!! Remember that path strings are very flexible - they can be relative or absolute. So a/b/c.txt is the same as a/b/../b/c.txt. The canonical form of any file is just the absolute path name, e.g. /home/someone/a.txt
* Better to leave the canonicalization to the programming language - which defers to the OS anyway). 
  * Java uses getCanonicalPath(), 
  * realpath() is the name in C, PHP, and Perl. 
* Tactic: canonicalize your sandboxed directory, canonicalize the final filename you are about to open, and compare the two strings.
 
Historical Examples
-------------------
* Apache Tomcat in [CVE-2009-2902](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2009-2902) allowed web applications be named "...war", which could be used for arbitrary file deletion outside of the webapp sandbox. See Tomcat's [report](http://tomcat.apache.org/security-5.html) and their [fix](http://svn.apache.org/viewvc?view=revision&revision=902650) (note: the fix includes multiple fixes, the [ExpandWar fix](http://svn.apache.org/viewvc/tomcat/tc5.5.x/trunk/container/catalina/src/share/org/apache/catalina/startup/ExpandWar.java?r1=902650&r2=902649&pathrev=902650) is particularly instructive).

Notes
-----

* This is common to web applications, especially. This often appears in PHP apps that delegate code to the operating system, or use flat file storage.
* Path Traversal is akin to SQL Injection where it's string concatenation gone wrong. Sadly, there's no version of a prepared statement for files (e.g. set the directory separately from the file name). 
  * Sadly, Java's `new File(sandbox, filename)` is still vulnerable to this.
* The myriad of exploits for this one over the years has shown that blacklisting is not a good approach. Better to just convert to absolute, and check the directory from there.
* Can also be a danger with configuration files. In the interest of defense in depth, it might be wise to do this kind of check when a properties file contains the name of another file.

Running the Demo
----------------
```sh
  cd path-traversal
  make
```
