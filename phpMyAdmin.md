# Setting up PHPMyAdmin

(used source as basis: https://wiki.crowncloud.net/?How_to_Install_PhpMyAdmin_in_Debian_12#Downloading+phpMyAdmin)

## Install PHPMyAdmin:

`sudo wget https://files.phpmyadmin.net/phpMyAdmin/5.2.1/phpMyAdmin-5.2.1-all-languages.tar.gz`

`sudo tar xvf phpMyAdmin-5.2.1-all-languages.tar.gz`

`sudo mv phpMyAdmin-5.2.1-all-languages /usr/share/phpmyadmin`

`sudo mkdir -p /var/lib/phpmyadmin/tmp`

`sudo chown -R www-data:www-data /var/lib/phpmyadmin`

## Create the config.inc.php in /usr/share/ from the sample:

`sudo cp /usr/share/phpmyadmin/config.sample.inc.php /usr/share/phpmyadmin/config.inc.php`

## Install a password generator:

`sudo apt install pwgen`

## Open a separate terminal and run the generator for a 32 characters long password:

`sudo pwgen -s 32 1`

## Open the config.inc.php file:

`sudo nano /usr/share/phpmyadmin/config.inc.php`

## Enter the string of 32 random characters from the password generator in between single quotes:

> $cfg['blowfish_secret'] = 'STRINGOFTHIRTYTWORANDOMCHARACTERS';

> /* YOU MUST FILL IN THIS FOR COOKIE AUTH! */

## Then uncomment this section:

> /* Storage database and tables */

> $cfg['Servers'][$i]['pmadb'] = 'phpmyadmin';

> $cfg['Servers'][$i]['bookmarktable'] = 'pma__bookmark';

> $cfg['Servers'][$i]['relation'] = 'pma__relation';

> $cfg['Servers'][$i]['table_info'] = 'pma__table_info';

> $cfg['Servers'][$i]['table_coords'] = 'pma__table_coords';

> $cfg['Servers'][$i]['pdf_pages'] = 'pma__pdf_pages';

> $cfg['Servers'][$i]['column_info'] = 'pma__column_info';

> $cfg['Servers'][$i]['history'] = 'pma__history';

> $cfg['Servers'][$i]['table_uiprefs'] = 'pma__table_uiprefs';

> $cfg['Servers'][$i]['tracking'] = 'pma__tracking';

> $cfg['Servers'][$i]['userconfig'] = 'pma__userconfig';

> $cfg['Servers'][$i]['recent'] = 'pma__recent';

> $cfg['Servers'][$i]['favorite'] = 'pma__favorite';

> $cfg['Servers'][$i]['users'] = 'pma__users';

> $cfg['Servers'][$i]['usergroups'] = 'pma__usergroups';

> $cfg['Servers'][$i]['navigationhiding'] = 'pma__navigationhiding';

> $cfg['Servers'][$i]['savedsearches'] = 'pma__savedsearches';

> $cfg['Servers'][$i]['central_columns'] = 'pma__central_columns';

> $cfg['Servers'][$i]['designer_settings'] = 'pma__designer_settings';

> $cfg['Servers'][$i]['export_templates'] = 'pma__export_templates';

## Add the following line to bottom of the file:

> $cfg['TempDir'] = '/var/lib/phpmyadmin/tmp';

## Finally, save & exit the file.

## Create a phpmyadmin.conf file:

`sudo nano /etc/apache2/conf-available/phpmyadmin.conf`

## Paste the following text into the file:

```
# phpMyAdmin default Apache configuration

Alias /phpmyadmin /usr/share/phpmyadmin

<Directory /usr/share/phpmyadmin>
    Options SymLinksIfOwnerMatch
    DirectoryIndex index.php

    <IfModule mod_php5.c>
        <IfModule mod_mime.c>
            AddType application/x-httpd-php .php
        </IfModule>
        <FilesMatch ".+\.php$">
            SetHandler application/x-httpd-php
        </FilesMatch>

        php_value include_path .
        php_admin_value upload_tmp_dir /var/lib/phpmyadmin/tmp
        php_admin_value open_basedir /usr/share/phpmyadmin/:/etc/phpmyadmin/:/var/lib/phpmyadmin/:/usr/share/php/php-gettext/:/usr/share/php/php-php-gettext/:/usr/share/javascript/:/usr/share/php/tcpdf/:/usr/share/doc/phpmyadmin/:/usr/share/php/phpseclib/
        php_admin_value mbstring.func_overload 0
    </IfModule>
    <IfModule mod_php.c>
        <IfModule mod_mime.c>
            AddType application/x-httpd-php .php
        </IfModule>
        <FilesMatch ".+\.php$">
            SetHandler application/x-httpd-php
        </FilesMatch>

        php_value include_path .
        php_admin_value upload_tmp_dir /var/lib/phpmyadmin/tmp
        php_admin_value open_basedir /usr/share/phpmyadmin/:/etc/phpmyadmin/:/var/lib/phpmyadmin/:/usr/share/php/php-gettext/:/usr/share/php/php-php-gettext/:/usr/share/javascript/:/usr/share/php/tcpdf/:/usr/share/doc/phpmyadmin/:/usr/share/php/phpseclib/
        php_admin_value mbstring.func_overload 0
    </IfModule>

</Directory>

# Authorize for setup
<Directory /usr/share/phpmyadmin/setup>
    <IfModule mod_authz_core.c>
        <IfModule mod_authn_file.c>
            AuthType Basic
            AuthName "phpMyAdmin Setup"
            AuthUserFile /etc/phpmyadmin/htpasswd.setup
        </IfModule>
        Require valid-user
    </IfModule>
</Directory>

# Disallow web access to directories that don't need it
<Directory /usr/share/phpmyadmin/templates>
    Require all denied
</Directory>
<Directory /usr/share/phpmyadmin/libraries>
    Require all denied
</Directory>
<Directory /usr/share/phpmyadmin/setup/lib>
    Require all denied
</Directory>
```

## Finally, save & exit the file.

## Enable the configuration:

`sudo a2enconf phpmyadmin.conf`

## Restart the Apache server:

`sudo systemctl reload apache2`

## Set privileges in the MariaDB databases:

`sudo mysql -uroot -p`

## Put these lines one after the other whith Enters:

`GRANT SELECT, INSERT, UPDATE, DELETE ON *.* TO 'pi'@'localhost' IDENTIFIED BY 'your_password';`

`GRANT ALL PRIVILEGES ON *.* TO 'pi'@'localhost' IDENTIFIED BY 'your_password' WITH GRANT OPTION;`

## Leave:

`quit`

## Add pi (or your user) to the www-data group:

`sudo usermod -a -G www-data pi`

## Change the owner of /var/www that Wordpress or any other web app can use it:

`sudo chown -R www-data:www-data /var/www`

## Set the right for the folder (777 is full access, set only if you use your server alone! Change accordingly if you want to publish your server.):

`sudo chmod -R 777 /var/www`

## If you copy a folder into /var/www/html, you have to run the right-setting chmod command above again!

## Enter phpMyAdmin in your browser:

`http://localhost/phpMyAdmin`

## Final setting of phpmyadmin database:

At the first time phpMaAdmin will tell you on the bottom with a link to the solution that the phpmyadmin database is not created (or so). Click on the link and create it. Then you are good to go and can create your databases.
