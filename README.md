# LAMP-on-Raspberry-Pi-Bookworm-with-PHP-7.4
LAMP on Raspberry Pi Bookworm with PHP 7.4 (for legacy Wordpress Theme versions)

## Use case:

I have an archived WordPress blog with a theme written in PHP 7.4, so it doesn't work with PHP 8. Unfortunately, Bookworm comes with PHP 8, that is, if I give the command `sudo apt install php -y` (which worked on Bullseye and installed everything of PHP 7.4) it will install PHP 8. So far so good, PHP 7.4 can be installed (only you have to install also some additional modules as you can see in the PHP74 file), but then the phpMyAdmin wont' work if it is installed with `sudo apt install phpmyadmin -y`. Unfortunately, phpMyAdmin must be installed manually, that's why the all fuss about it.

But if you follow these steps in the files, it will work perfectly with php 7.4 themes. I run WordPress 6.6.2 also with a Twenty-Sixteen Theme and it also works fine.

So, the steps are:

## 1. FTP Server

Just for convenience if you want to upload some files with codes upfront, to be able to copy them into the terminal.

## 2. Apache Server

## 3. PHP74

## 4. MariaDB

## 5. WordPress

## 6. phpMyAdmin

After this, you can install WordPress from scratch, or upload the existing blog's folder into /var/www/html (don't forget to set www-data as owner and chmod the folder), and with phpMyAdmin create the blog's database and import it's sql dump (which you exported from the blog's existing database previously). If you change the IP address of the blog, run a Replace all command from the old to the new IP in the dump sql file before import it, in a text editor like Notepad++. Don't forget to set the proper database name and login info in the wordpress config file.

Have fun!
