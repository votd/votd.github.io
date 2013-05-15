---
layout: catalog
tags: web
---

Open Redirect
=============

Description
-----------

See [CWE-601](http://cwe.mitre.org/data/definitions/601.html)

Mitigations
-----------
* Input validation, particularly whitelisting, although more than just validating character strings - look up the URL itself. Make your whitelist a set of known, safe, URLs within your app. Only allowing input that redirects to your own site is also a big step.
* Like file paths and path traversal vulnerabilities, URLs can get pretty complicated. Java has a `normalize()` method in the [URI](http://docs.oracle.com/javase/7/docs/api/java/net/URI.html#normalize%28%29) class that helps you canonicalize your URL before checking it. This is especially helpful if you are in an untrusted site situation (e.g. your webapp is hosted on the same site as untrusted webapps and you want to block intra-site redirects like `../evilsite`). 

Historical Examples
-------------------
* The popular bug tracking engine Trac had one of these. See [CVE-2008-2951](http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2008-2951) and its [fix](http://trac.edgewall.org/changeset/7224/branches/0.10-stable)
 
Notes
-----
* While our example uses a form post, exploits more often occur in URL parameters (e.g. `http://yourwebsite.com/somethingvulnerable.jsp?redirect=www.evilwebsite.com`)
* Detecting this one is the hard part. Most usages of redirects are when the URLs are not connected to user input (and are therefore safe). But, whenever user input eventually leads to a redirect, consider this issue.
* This is a popular vulnerability used in phishing attacks (i.e. social engineering). Suppose PayPal had an open redirect vulnerability. Then an attacker could spam people asking them to check their paypal accounts. The URLs start with `paypal.com`, so most users would consider them safe and click through.

Running the Demo
----------------
Using the XAMPP installation, place the JSP page from the `open-redirect` directory into the `xampp-portable/tomcat/webapps/open-redirect/` and go to http://127.0.0.1:8080/open-redirect/open-redirect.jsp folder.

