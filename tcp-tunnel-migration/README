## Migration script for tcp socket to unix file socket

To install the script download the file to `/usr/local/bin/clp-migrate-php-fpm-socket` then give it the execute flag using `chmod +x /usr/local/bin/clp-migrate-php-fpm-socket`. You can then run the command in bash by simply calling `clp-migrate-php-fpm-socket`. 

The script will list all PHP sites and allow you to pick which one you want to migrate.

### Disclaimer

The script is provided as is. It is in an early state and it does edit files on the system. It's best to make a backup or snapshot of the VPS before running the system. The files it touches/edits are:
- The CloudPanel database in `/home/clp/htdocs/app/data/db.sq3`
- The PHP pool configuration created by CloudPanel for the site which is located in the `/etc/php/PHP_VERSION/fpm/conf.d/` folder where `PHP_VERSION` is the PHP version of the site. The file is named like the domain with a `.conf` extension.
- The nginx site configuration on the disk in `/etc/nginx/sites-enabled/`. The file is also named like the domain name with an `.conf` extension.

After the edit the PHP-FPM process and nginx are reloaded. If errors occur then the services will not start again and you will need to fix or restore these files.

### Checking if it worked

To test if it worked you can see the socket in `/var/run/php/` with the domain as the name of the file and owned by the site user and group. You should also see the fastcgi_pass line in the vhost and the CloudPanel UI to be changed to the socket path.
