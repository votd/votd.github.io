---
layout: catalog
---

Log Neutralization
==================

Description
-----------

* See [CWE-117](http://cwe.mitre.org/data/definitions/117.html)
* If you allow newlines in your logs, then attackers can forge log entries, throwing investigations off. Related to generalized CRLF Injection ([CWE-93](http://cwe.mitre.org/data/definitions/93.html)) 

Mitigations
-----------
* Don't allow newlines in your logs - remove them entirely.
* Depending on what tools are used to analyze logs, the CRLF character might not be enough. Consider <br> if you can view logs online, too.
* Don't forget to log the situation where a newline is injected, too.

Historical Examples
-------------------
* PayPal had this issue hit them in [CVE-2006-0201](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2006-0201) 
 
Notes
-----
* This is one vulnerability that is explicitly a repudiation threat.
* By itself, this is pretty innocuous. In conjunction with other attacks, an attacker can provide misinformation in the logs that throws off the post-exploit investigation.
* Developers who have access to previous logs (or similar logs) can easily guess or reverse-engineer your patterns, making the result indistinguishable. Take a look at [CAPEC attack pattern 93](http://capec.mitre.org/data/definitions/93.html).
* Oddly enough, common logging libraries like `java.util.logging` and `log4j` don't have an option to remove newlines.
 

Running the Demo
----------------
{% highlight sh %}
  cd log-neutralization
  ./make
{% endhighlight %}

Note that it's `./make`, not `make`
