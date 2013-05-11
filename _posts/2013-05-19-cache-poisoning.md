Cache Poisoning
================

Description
-----------

See [CAPEC-141](http://capec.mitre.org/data/definitions/141.html) attack pattern

Mitigations
-----------
* If possible, don't allow users to set their own cache expiration dates
* If possible, don't allow users much control over caches to begin with
* As always, input validation helps, but it should not comprise the whole solution.
* If you implement your own cache, be sure to put some extra checks in place for expiration dates and purging policies. Build the feature so that the expiration date is not set by the user, or at the very least validated to a specific range. If it's worth the performance hit, periodically purge the cache regardless of expiration dates.

Historical Examples
-------------------
* A very famous vulnerability, [CVE-2008-1447](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2008-1447) in BIND, a DNS protocol that runs at the heart of the internet, had a cache poisoning vulnerablitity that went undiscovered for decades until it was found and actively exploited in 2008. DNS maps names to IP addresses and uses a complex, multi-tiered form of caching throughout the internet's root nodes. Attackers were able to cause certain domain names (Yahoo was one of them) to map to different servers on malicious IP addresses for some users, depending on your nearest DNS host.
* A similar vulnerability in dnscache [CVE-2008-4392](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2008-4392) attacked the "Start of Authority" requests. The [reports](http://www.your.org/dnscache/) show some relatively simple patches ([this](http://www.your.org/dnscache/0001-dnscache-merge-similar-outgoing-queries.patch) and [this](http://www.your.org/dnscache/0002-dnscache-cache-soa-records.patch)) that essentially do input validation and handle the boundary cases better.

Notes
-----
* If your system's assets are cached, then your cache becomes an asset. Consider this possibility in your risk analysis and planning for new features.
* Historically, cache poisoning has most often applied to networking situations. The concept, however, is not specific to networking.
* Cache poisoning can also occur in a web applications if the attacker can set HTTP headers. In particular, setting HTTP headers like Last-Modified can fool both the victim's browser cache and server-side caches (e.g. Squid) into keeping exploits like XSS and CSRF cached for multiple requests. To mitigate this, never allow user data to be used in HTTP response headers.
* In the security community, this is often considered more of an attack than a vulnerability, as often the mistake is not in the cache itself, it's in the surrounding systems that employ the cache.

Running the Demo
----------------
```sh
  cd cache-poisoning
  make
```

