---
layout: catalog
---

Hashing without Salt
====================

Description
-----------

* See [CWE-759](http://cwe.mitre.org/data/definitions/759.html)
*  If an attacker breaks in to a system that provides authentication, they should not be able to access the passwords. Historically, people would hash (digest) algorithms to accomplish this. However, commonly-guessed passwords are still vulnerable, as attackers can make "rainbow tables", or digests of common passwords. 

Mitigations
-----------
* Append a secret "salt" string that only the server knows before digesting. This will make those digests unrecognizable.
* Make sure that the salt is set by the final user, not hardcoded or set by default. Server salt is like default passwords or PRNG seeds - secrets that users should set by default.

Notes
-----
* Don't store passwords in plain text. This means that your "reset password" feature, should never email passwords in plaintext (because you don't have that anymore!). If you ever notice a website that does this, they are not hashing their passwords. 
* Don't make your salt easily guessable. Any long string is fine, since it's stored you won't need to remember again.

Running the Demo
----------------
```sh
  cd hashing-salt
  make
```

* The given example is an authentication example that demonstrates the different ways you can store a password and still authenticate. User sets their password, which gets salted and then digested (hashed). Every time the user authenticates, the system then salts and digests the password, and checks the results.

