# Setting up and FTP server

## Install the server:

`sudo apt install vsftpd`

## Open the config file:

`sudo nano /etc/vsftpd.conf`

## Add or uncomment or uncomment and change:

```
listen=YES
anonymous_enable=NO
local_enable=YES
write_enable=YES
local_umask=022
chroot_local_user=YES
user_sub_token=$USER
local_root=/home/$USER/FTP
```

## Create the directory which is used for file transfer (pi or replace it with your user):

`mkdir -p /home/pi/FTP/files`

## Give rights to the directory (pi or replace it with your user):

`chmod a-w /home/pi/FTP`

## Restart the server:

`sudo service vsftpd restart`
