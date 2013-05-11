---
layout: catalog
---

Log Overflow
============

Description
-----------

* See [CWE-400](http://cwe.mitre.org/data/definitions/400.html) for a general description.
* Related CWEs are [CWE-779](http://cwe.mitre.org/data/definitions/779.html) CWE-779 and [CWE-770](http://cwe.mitre.org/data/definitions/770.html)
* Printing out to a console or logger usually ends up in a text file. If an attacker knows this, and the logging is unrestricted, then attackers can fill up the log file and crash the machine by filling up the hard drive. This is a denial of service attack that is particularly difficult to recover from. Plus, weird things happen when the entire hard drive is completely out of bytes, so attackers can take advantage of this. 

Mitigations
-----------

* Use a properly-configured logging library (e.g. log4j). In configuring your logger, be sure to use rolling log files. These can be rotated on a daily basis, or by size. Be sure to actually test this functionality yourself.
* Don't log so much. Separate out the debugging logs from useful logs. Don't ship with debugging information turned on.


Historical Examples
-------------------
* The Linux kernel has had this issue in a myriad of forms. In [CVE-2013-0231](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2013-0231), a certain driver was flooding the kernel with messages and [the fix](https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/commit/?id=51ac8893a7a51b196501164e645583bf78138699) was to handle the error another way than just printing a message.

Notes
-----

* Don't forget to inspect configuration files! You can have vulnerabilities there too.
* Mostly an issue in applications that run on servers, although desktop clients are not immune to this
* The disadvantage of this mitigation is that you can potentially lose your logs if they get over-rotated. Attackers can potentially take advantage of this fact by intentionally overflowing the logs to erase the evidence. But other protections, like request limits, can mitigate that problem too.
* As a general rule, avoid unlimited hard drive storage (e.g. uploading photos). Sometimes it's easier to just store images as BLOBS in a database (where the table sizes are often limited by default), as opposed to dealing with the OS directly.

Running the Demo
----------------
{% highlight sh %}
  cd log-overflow
  make
{% endhighlight %}
