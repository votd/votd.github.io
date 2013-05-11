SQL Injection
=============

Description
-----------

See [CWE-89](http://cwe.mitre.org/data/definitions/89.html)

Historical Examples
-------------------
* The ActiveRecord ORM used in Ruby on Rails has had a few of these over the years. One early SQL injection vulnerability was [CVE-2008-4094](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2008-4094), via the :limit and :offset fields. See the [issue]() and [patch](http://s3.amazonaws.com/activereload-lighthouse/assets/43f904c57ff3092f8f879ea997439190c1c90678/0001-adding-sql-injection-fixes-for-limit-and-offset.patch?AWSAccessKeyId=1AJ9W2TX1B2Z7C2KYB82&Expires=1366897315&Signature=a6XeVe1Jl1tYs2Cl%2FH33Y0fwPVk%3D). 

Mitigations
-----------

* The *only* acceptable mitigation are properly-used prepared statements. These API calls are supported by all SQL standards, and separate the logic of the query from its input entirely (i.e. pre-compile the SQL). No string concatenation should be used. The key: don't allow any possibility to let user input turn into executable code.
* Escaping characters has proven to be a poor substitute, as changing character sets makes this a moving target and quite hard.
* Using an OO-relational mapper (e.g. Hibernate) can mitigate this. However, string concatenation on the Hibernate query language can result in basically the same thing.

Notes
-----
* Currently the top problem on the CWE Top 25 vulnerabilities. Very common today.
* Can be done in pretty much all languages that can execute SQL: Java, Ruby, PHP, etc.
* Not particularly hard to find or fix, you just have to know about it.
* A lot of people will tell you that you need lots of tools to fix SQL injection. It's all snakeoil... just use properly use prepared statements with binding variables.
* See this [classic XKCD](http://xkcd.com/327/)


Running the Demo
----------------
```sh
  cd sql-injection
  make
```

