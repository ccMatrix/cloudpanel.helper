# Connect wildcard certificate obtained by acme.sh to CloudPanel sites

## Install incrontab

Use `apt install incron` to install incron. It will listen to inode changes and can run commands on different inode events

## Install the script

Copy the file `clp-install-certificate` to `/usr/local/bin/` and change the variables inside to match the path to your acme.sh

## Setup acme.sh

Install and setup [acme.sh](https://github.com/acmesh-official/acme.sh) to obtain certificates. Use the command `/usr/local/bin/clp-install-certificate && service nginx force-reload` to connect the new certificates and reload nginx after a new Let's Encrypt certificate was obtained.

## Setup incron

Run `incrontab -e` in your SSH terminal to open the editor. Then add the line:
```
/etc/nginx/sites-enabled/       IN_CREATE                       /usr/local/bin/clp-install-certificate $#
```
This will trigger the script whenever a new site is created in CloudPanel. The clp-install-certificate will get the filename of the config and extract the domain from the filename and install the acme.sh wildcard certificate for it.
