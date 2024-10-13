# Install PHP 7.4

Under Bookworm the default PHP version is the 8. If you have an application, like Wordpress, which uses PHP 7.4 and you don't want to update it, you have to install PHP 7.4 manually.

## Get the package:

`sudo apt update`

`sudo apt -y install lsb-release apt-transport-https ca-certificates`

`sudo wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg`

`echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | sudo tee /etc/apt/sources.list.d/php.list`

## Install PHP:

`sudo apt update`

`sudo apt list --upgradable`

`sudo apt -y install php7.4`

## Install the modules which are needed additionally for WordPress:

`sudo apt  install -y php7.4-mysqli`

`sudo apt install -y php7.4-mbstring`

`sudo apt  install -y php7.4-curl`

`sudo apt install -y php7.4-gd`

`sudo apt install -y php7.4-imagick`

## Check the installed PHP version:

`php -v`

## Create an index.php file:

`sudo nano /var/www/html/index.php`

## Put this line in the new empty index.php file and save file:

> `<?php phpinfo(); ?>`

## Delete the index.html to be able to use index.php:

`sudo rm /var/www/html/index.html`

## Restart the Apache server:

`sudo service apache2 restart`
