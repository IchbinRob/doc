# Global Lamp doc

## MariaDB
### PhpMyAdmin

### CLI
#### Create User

#### Create database
- `sudo mariadb`
- `CREATE DATABASES my_db_name;`
- `GRANT ALL ON my_db_name.* TO 'user'@'localhost' IDENTIFIED BY 'password' WITH GRANT OPTION;`

#### Import database
- `mysql -u username -p my_db_name < data-dump.sql`

#### Edit Database
##### Wordpress wp_option exemple : 
- `sudo mariadb`
- `use my_db_name;`
- Update table : 
```sql UPDATE wp_options 
SET option_value = 'url'
WHERE option_name = 'siteurl';```
- repeat with `home` option_name

## Apache

### Vhost
config dispo : /etc/apache2/site-available
config active : /etc/apache2/site-enabled
Activer une config : 
 - `cd /etc/apache2/site-available`
 - `a2ensite my-site.conf`
 - `systemctl reload apache2`

### Add SSL with let's encrypt
[Digital Ocean Tuto](https://www.digitalocean.com/community/tutorials/how-to-secure-apache-with-let-s-encrypt-on-ubuntu)


