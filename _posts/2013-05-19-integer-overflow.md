---
layout: catalog
---

Integer Overflow
================

Description
-----------
See [CWE-190](http://cwe.mitre.org/data/definitions/190.html)

Historical Examples
-------------------
* From Firefox, see [CVE-2010-2753](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2010-2753) and the corresponding [Bugzilla](https://bugzilla.mozilla.org/show_bug.cgi?id=571106) and [patch to fix](https://bug571106.bugzilla.mozilla.org/attachment.cgi?id=451552&action=diff&collapsed=&context=patch&format=raw&headers=1)

Mitigations
-----------
* Check the size of your integers, considering what would happen if it wrapped around
* Watch the casting - don't just ignore those compiler warnings!
* Libraries such as SafeInt or BigInteger might be more suitable if the problem is very complex. 
* Having a well-placed integrity check built into your design can reduce the messiness of checking every single operation.

Notes
-----
* A wraparound combined with a malloc operation can result in a zero-sized buffer being allocated - leading to a zero-byte buffer, which will always be overflowed.
* In practice, most integer wraparounds come from improper casting, not as much from math operations.
* Always checking every integer for wraparound after every arithmetic operation is impractical. Pay attention to which integers wrapping around would have security implications. 
* Wraparound doesn't have security effects on every integer, but on more than you may think. 

Running the Demo
----------------
{% include demo_default.md %}