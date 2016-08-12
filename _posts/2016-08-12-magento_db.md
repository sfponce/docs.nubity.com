### Description

Monitor your Magento purchase workflow through the database.

Features:

*   Items added to a cart per minute.
*   Invoices created per minute.
*   Orders created per minute.
*   Quotes created per minute.

### Requirements

*   MySQL user with read-only access to Magento DB
*   `Python` >= `2.6`
*   `PyMySQL` Python module
*   `PyYAML` Python module
*   `simplejson` Python module

### Setup

1.  Create the read-only MySQL user:
```bash
mysql> GRANT SELECT ON magentoDB.* TO 'nubity'@'127.0.0.1' IDENTIFIED BY 'strongPassword';
```
    _Note: Replace magentoDB with your real magento database name._

2.  Run `nubity-cli` to set MySQL credentials created above:
```bash
$ sudo /usr/sbin/nubity-cli
```

    Choose option 1: MySQL Database Login

    Insert your MySQL connection details

3.  Run `nubity-cli` to set Magento Database name:
```bash
$ sudo /usr/sbin/nubity-cli
```

    Choose option 2: Magento MySQL Database.

    Insert your Magento Database Name.
