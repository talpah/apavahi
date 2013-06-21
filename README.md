apavahi
=======

You need to have:
---
- Apache
- mod-dnssd
- Avahi

Steps:
---
1.  Create your document root(s) and note the path(s)
2.  Run create-apache-vhost for each one (just run it without params to see the usage)
3.  Run publish-apache-aliases

Explanations:
---
- create-apache-vhost       - creates and activates a vhost in apache with specified data
- publish-apache-aliases    - gets all non-local ".local" Web Services from Avahi and passes them to addalias.py
- addalias.py               - pushes CNAME records to Avahi for specified aliases



Authors:
---
addalias.py (avahi-alias.py) by gdamjan. Copied from https://gist.github.com/gdamjan/3168336
