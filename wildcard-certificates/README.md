# Connect wildcard certificate obtained by acme.sh to CloudPanel sites

## Install incrontab

Use `apt install incron` to install incron. It will listen to inode changes and can run commands on different inode events

## Install the script

Copy the file `connect-certificates` to `/usr/local/bin/` and change the variables inside to match the path to your acme.sh

## Setup acme.sh

Install and setup acme.sh to obtain certificates. Use the command `/usr/local/bin/connect-certificates && service nginx force-reload` to connect the new certificates and reload nginx after a new Let's Encrypt certificate was obtained.

## Setup incron

Run `incrontab -e` in your SSH terminal to open the editor. Then add the line:
```
/etc/nginx/ssl-certificates/    IN_MODIFY,IN_DONT_FOLLOW        /usr/local/bin/connect-certificates $@/$#
```
This will trigger the script on any change to certificates. So if a new site is generated in CloudPanel and a new self signed certificate is created it will be overwritten.
