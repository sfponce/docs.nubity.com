---
title: Apache HTTPD
section: Web Servers
index: 2
tag:
- webserver
- lamp
---
## Description

It gathers performance metrics about Apache web server.

Features:

*   Number of slots/threads in every status:
    *   Waiting for connection.
    *   Sending reply.
    *   Reading request.
    *   Starting up.
    *   Open slot with no current process.
    *   Keepalive (read).
    *   Closing connection.
    *   Gracefully finishing.
    *   Idle cleanup of worker.
    *   DNS Lookup.
    *   Logging.
*   Request per second.
*   Total count of idle & busy workers
*   Total available slots
*   Bytes received/sent

## Requirements

Apache server-status page has to be enabled and accessible from localhost.

## Setup

1.  Enable server-status module in Apache config file.

    Add this configuration block to `/etc/httpd/conf/httpd.conf`

    ```
    ExtendedStatus on
    <Location /server-status>
        SetHandler server-status
        Order deny,allow
        Deny from all
        Allow from 127.0.0.1
    </Location>
    ```
    Usually this block already exists but it's commented out so you only have to remove the comment character ("#") in front of each line.


2.  If your site has rewrite rules, you should create a dedicated virtual host (_vhost_) for server-status requests.

    Otherwise, your site could capture the server-status request and redirect it to your home or somewhere else.

    Add this vhost to `httpd.conf` at the end of the file to avoid any issue in the vhost matching order:

    ```
    <VirtualHost *:80>
    ServerName status.local
    DocumentRoot /var/www/html/status
    <Directory /var/www/html/status>
    AllowOverride All
    Options -Indexes
    </Directory>
    ErrorLog logs/status.orgullorojo.com-error_log
    CustomLog logs/status.acento.com-access_log combined
    </VirtualHost>
    ```

3.  Force the resolution of the host `status.local` in file `/etc/hosts`

    ```bash
    $ sudo 'echo 127.0.0.1    status.local' >> /etc/hosts
    ```

4.  Restart Apache/HTTPD

    ```bash
    $ sudo service restart httpd
    ```
