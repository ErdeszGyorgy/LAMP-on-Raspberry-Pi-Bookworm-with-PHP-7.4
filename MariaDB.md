# Setup the MariaDB database

## Install MariaDB

`sudo apt-get install mariadb-server php-mysql -y`

## Restart the Apache server:

`sudo service apache2 restart`

## Set some security settings:

`sudo mysql_secure_installation`

Go through the dialogue:

> Enter current password for root (enter for none): press Enter

> Switch to unix_socket authentication [Y/n]: n

> Change the root password? [Y/n]: n

> Remove anonymous users? [Y/n]: Y

> Disallow root login remotely? [Y/n]: Y

> Remove test database and access to it? [Y/n]: Y

> Reload privilege tables now? [Y/n]: Y

When complete, you will see the message:

> All done! and Thanks for using MariaDB!
