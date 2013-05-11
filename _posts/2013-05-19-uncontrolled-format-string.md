---
layout: catalog
---

Uncontrolled Format String
==========================

Description
-----------

* See [CWE-134](http://cwe.mitre.org/data/definitions/134.html)
* In C, printing using `printf(str)` instead of `printf("%s", str)` results in the user being able to control the format string. This is especially egregious when you look at the `%x` and `%n` codes, which allow users to read and write arbirary bytes to arbitrary memory locations. 

Mitigations
-----------
* Just use a format string!
* Watch your compiler warnings, which look like: `warning: format not a string literal and no format arguments` 

Historical Examples
-------------------
* PHP once had a vulnerablity disclosure fixing 27 of these. The issue was in mishandling the throwing of exceptions. See [CVE-2011-1153](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2011-1153) and [the fix](http://svn.php.net/viewvc/php/php-src/trunk/ext/phar/phar_object.c?r1=309221&r2=309220&pathrev=309221) along with [the Red Hat Bug with an exploit](https://bugzilla.redhat.com/show_bug.cgi?id=688378).
 
Notes
-----
* These are very common coding mistakes. Blogs, forums, Q&A sites all will commonly have format string vulnerabilities in their code snippets about something else, which developers will foolishly copy-and-paste into production code.    
* The key to the exploit that makes the `%x` code work is that `printf` is a varargs function. If you add more `%x` codes to the string, `printf` just starts reading memory locations from where it left off - right at the call stack.
* This one is just as severe as buffer overflow, as it can allow arbitrary remote code execution.
* [Entire books](http://www.amazon.com/Buffer-Overflows-Format-String-Schwachstellen-Tobias-Klein/dp/3898641929/) have been written on elaborate exploits of format string vulnerabilities.

Running the Demo
----------------
```sh
  cd format-string
  make
  ruby read-memory.rb
```
