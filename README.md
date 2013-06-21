apavahi
=======
Use Avahi to provide DNS resolving for local development. This set of scripts allows 
using a single machine with multiple vhosts. All ServerNames will be in the form of _vhost_.local.

You need to have:
---
On development server/vm:
> - Linux
> - Apache
> - mod-dnssd
> - Avahi

On Linux clients:
> - Avahi

On Windows clients:
> - Bonjour from Apple or something similar

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
