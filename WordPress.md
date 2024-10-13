# WORDPRESS preparation

## Set the rewrite mode:

`sudo a2enmod rewrite`

## Restart the Apache server:

`sudo systemctl restart apache2`

## Adjusting Apache's config file:

`sudo nano /etc/apache2/sites-available/000-default.conf`

## Add the following lines after line 1:

```
<Directory "/var/www/html">

  AllowOverride All

</Directory>
```

## Ensure it’s within the <VirtualHost *:80> like so:

```
<VirtualHost *:80>

    <Directory "/var/www/html">

        AllowOverride All

    </Directory>

    ...
```

## Finally, save & exit the file.

## Restart the Apache server:

`sudo service apache2 restart`

## Open the php.ini file under for Apache2:

`sudo nano /etc/php/7.4/apache2/php.ini`

## Change the following settings to higher values like these (or what is suitable for you):

> `post_max_size = 800M`

> `upload_max_filesize = 800M`

> `max_execution_time = 5000`

> `max_input_time = 5000`

> `memory_limit = 2048M`

## Finally, save & exit the file.

## Restart the Apache server:

`sudo service apache2 restart`
