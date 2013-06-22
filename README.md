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
(First time usage run all steps; Subsequent usages should only run step 4; When adding new vhosts, go from 2)

1.  Enable mod-dnssd in Apache
2.  Create your document root(s) and note the path(s)
3.  Run create-apache-vhost for each one (just run it without params first to see the usage)
4.  Run publish-apache-aliases (note that this process will not terminate unless told so, with Ctrl-C)

Caveats:
---
- By default, on debian and friends, mod-dnssd should come with the following configuration. If not, make it happen.

```apache
# This is the config file for mod_dnssd.

<IfModule mod_dnssd.c>
    DNSSDEnable On
    DNSSDAutoRegisterVHosts On
</IfModule>
```
- In order for Apache to propagate names through mod-dnssd, Avahi must be started. If you plan to 
    use this feature on boot, you must ensure Apache service is started after Avahi. 
    On Debian, you might need to adjust the LSB headers for the Apache init script (/etc/init.d/apache2), 
    by adding "avahi" at the end of the "Required-Start" tag, and then run "update-rc.d apache2 defaults" 
    as root, to reorder the startup sequence.


Explanations:
---
- create-apache-vhost       - creates and activates a vhost in apache with specified data
- publish-apache-aliases    - gets all non-local ".local" Web Services from Avahi and passes them to addalias.py
- list-avahi-web-services   - lists all non-local ".local" Web Services from Avahi
- addalias.py               - pushes CNAME records to Avahi for specified aliases
- template.http             - this contains the Apache vhost template that will be used to create all new hosts


Authors:
---
addalias.py (avahi-alias.py) by gdamjan. Copied from https://gist.github.com/gdamjan/3168336
