---
layout: catalog
---

Java Reflection Abuse
=====================

Description
-----------

* See [CWE-470](http://cwe.mitre.org/data/definitions/470.html)
* Despite what you might assume, Java allows you to access private variables in other classes via its Reflection API. In untrusted API situations (e.g. plug-in architectures), this can lead to malicious libraries accessing and tampering with sensitive data.  

Mitigations
-----------
* Use the Java Security Manager to limit privileged API situations. While this feature is turned off by default, it's actually critical for deploying a Java application securely (e.g. in a servlet container) where an utrusted API situation is in effect.

Historical Examples
-------------------
* The ColdFusion database access APIs has had this vulnerability ([CVE-2004-2331](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2004-2331))
* In 2012 and 2013, Java has had some severe vulnerabilities where the security manager was bypassed. In particular, [CVE-2013-0422](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2013-0422), [CVE-2012-4681](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-4681), and [CVE-2012-3174](https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2012-3174) are all related to bugs in the Reflection API that bypasses the security manager and allows this abuse. In particular, bug [894172](https://bugzilla.redhat.com/show_bug.cgi?id=894172) at Red Hat is instructive, as well as two fixes at OpenJDK: [ecc14534318c](http://hg.openjdk.java.net/jdk7u/jdk7u-dev/jdk/rev/ecc14534318c) and [d9969a953f69](http://hg.openjdk.java.net/jdk7u/jdk7u-dev/jdk/rev/d9969a953f69). 
 
Notes
-----
* Many Java servers utilize a strict, security policy (e.g. [Tomcat](http://tomcat.apache.org/tomcat-7.0-doc/security-manager-howto.html)), however, many default installations of such servers do not force you to set up your security policy with the Java virtual machine.
* The Java security manager blocks all kinds of other sensitive actions, such as `System.exit(1);`, file system access, or using reflection to instantiate singletons.
* The Deployment & Distribution lecture covers more details on the Java Security Manager

Running the Demo
----------------
```sh
  cd java-reflection-abuse
  make
  make safe
```

