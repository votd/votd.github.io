---
layout: catalog
---

OS Command Injection
====================

Description
-----------

See [CWE-78](http://cwe.mitre.org/data/definitions/78.html)

Historical Examples
-------------------
* Apache HTTPD for Windows [had an issue with this](http://www.apacheweek.com/issues/02-03-22#security) where they allowed the pipe (|) character. Here's the [SVN commit](http://svn.apache.org/viewvc?view=revision&sortby=rev&revision=94092) for the fix, which involves additional logic for escaping characters.
* Ruby's `lib/curl.rb` gem allowed shell metacharacters. See the [report with an exploit](http://packetstormsecurity.com/files/120778/Ruby-Gem-Curl-Command-Execution.html).

Mitigations
-----------
* Many languages allow limiting an OS call to a single command, which can limit the injection.
* Generally speaking, be very careful with OS calls. Avoid, if possible. Usually, APIs exist that can accomplish the same thing.
* Only allow certain input to these commands, as opposed to blocking or escaping bad output.

Notes
-----
* Web application technologies like PHP and Ruby on Rails make these OS calls very easy these days. These are very dangerous, as getting access to the underlying web server can have a huge impact.
* It's tempting to think you can just use a quick grep function or call a separate script, but be sure to think twice about that interaction.

Running the Demo
----------------
```sh
  cd os-command-injection
  make
```

