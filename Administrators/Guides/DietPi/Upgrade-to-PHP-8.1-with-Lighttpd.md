## Before you start
- This tutorial was developed for and tested with DietPi 8.12.1 on a RaspberryPI.
- This tutorial only works if you use "Lighttpd" as webserver.
  Run `dietpi-software` and check the setting for "Webserver Preference".
- DietPi may behave differently on other systems.
- Nextcloud 24 is required _before_ upgrading to PHP 8.1.
- _Make sure to make a backup of your entire DietPi Instance (config, data, etc.) before you do this._



## Log in as Root
If you're using SSH, log in with `ssh root@<your dietpi ip>`.
If you're directly on the device, use `sudo su`



## Add PHP Package Archive
Execute the following commands on your DietPi to add the repository PHP 8.1 from [deb.sury.org](https://deb.sury.org/#php-packages):

```bash
# Add the PHP PPA from deb.sury.org
apt-get -y install apt-transport-https lsb-release ca-certificates curl
curl -sSL -o /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
apt-get update
```



## Install PHP 8.1
Execute the following command on your DietPi to install PHP 8.1:

```bash
# Remove conflicting packages
apt-get -y remove php-apcu php-igbinary php-redis

# Install PHP 8.1
apt-get -y install php8.1-common php8.1-fpm php8.1-cli php8.1-opcache php8.1-apcu php8.1-mysql php8.1-xml php8.1-zip php8.1-mbstring php8.1-gd php8.1-curl php8.1-redis php8.1-intl php8.1-bcmath php8.1-gmp php8.1-imagick php8.1-igbinary php8.1-readline php8.1-phpdbg imagemagick
```



## Update the PHP 8.1 configuration
Now you need to copy and edit the php-fpm configuration for PHP 8.1

Run `cp /etc/php/7.4/fpm/pool.d/www.conf /etc/php/8.1/fpm/pool.d/www.conf` to copy the existing configuration file.

Run `nano /etc/php/8.1/fpm/pool.d/www.conf` to open the configuration file.

You can use `CTRL` + `w` to search in the file,
with `CRTL` + `o` you can save the changed file and
with `CRTL` + `x` you can close the editor.

Find the following line:
```bash
listen = /run/php/php7.4-fpm.sock
```
and replace it with this line:
```bash
listen = /run/php/php8.1-fpm.sock
```
Then save the file and exit the editor.


Now execute the following command on your DietPi to link the DietPi configuration for PHP from PHP 7.4 to 8.1 and enable it:
```bash
# Enable the image magick module
# Errors related to PHP 7.4 can be ignored
phpenmod imagick

# Symlink NCP PHP configuration
ln -s /etc/php/7.4/mods-available/dietpi-nextcloud.ini /etc/php/8.1/mods-available/dietpi-nextcloud.ini
ln -s /etc/php/7.4/mods-available/dietpi.ini /etc/php/8.1/mods-available/dietpi.ini
phpenmod dietpi
phpenmod dietpi-nextcloud
```

Now you need to edit the configuration of PHP FPM.
Run the command `nano /etc/php/8.1/fpm/php.ini` to open a text editor with the config file.

You can use `CTRL` + `w` to search in the file, with `CRTL` + `o` you can save the changed file and with `CRTL` + `x` you can close the editor.

Find the line

```bash
;cgi.fix_pathinfo=1
```
and remove the `;` at the beginning so that the line reads 
```bash
cgi.fix_pathinfo=1
```

Then save the file, exit the editor and restart the PHP FPM service.
```bash
# Restart PHP
service php8.1-fpm restart
```



## Set up Lighttpd for PHP 8.1
Run the command `update-alternatives --config php-fpm.sock` to select which PHP version should be used for the webserver.
Select the option with the path "/run/php/php8.1-fpm.sock". If that option already has the asterisk ("*"), you can just enter "*" and confirm.

```bash
root@DietPi:~# update-alternatives --config php-fpm.sock
There are 2 choices for the alternative php-fpm.sock (providing /run/php/php-fpm.sock).

  Selection    Path                      Priority   Status
------------------------------------------------------------
* 0            /run/php/php8.1-fpm.sock   81        auto mode
  1            /run/php/php7.4-fpm.sock   74        manual mode
  2            /run/php/php8.1-fpm.sock   81        manual mode

Press <enter> to keep the current choice[*], or type selection number: 0
```

Then just restart lighttpd:
```bash
service lighttpd force-reload
```



## Set the PHP command line version
By default, your DietPi should now be using PHP 8.1.
You can check this by running `php -v`. The output should look like this:
```bash
root@DietPi:~# php -v
PHP 8.1.13 (cli) (built: Nov 26 2022 14:27:02) (NTS)
Copyright (c) The PHP Group
Zend Engine v4.1.13, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.13, Copyright (c), by Zend Technologies
```

It's important that it shows `PHP 8.1.*`. If it doesn't, you should run `update-alternatives --config php` and set PHP 8.1 as default:
```bash
root@DietPi:~# update-alternatives --config php
There are 2 choices for the alternative php (providing /usr/bin/php).

  Selection    Path             Priority   Status
------------------------------------------------------------
* 0            /usr/bin/php8.1   81        auto mode
  1            /usr/bin/php7.4   74        manual mode
  2            /usr/bin/php8.1   81        manual mode

Press <enter> to keep the current choice[*], or type selection number:0
```



## Check for Nextcloud and App updates
```bash
# Check for updates
ncc update:check

# Install updates of the passwords app if available
ncc app:update passwords
```



## Notes
- It can take a day before app updates show up in the apps store



# How to Switch back to PHP 7.4
Run the command `update-alternatives --config php-fpm.sock` to select which PHP version should be used for the webserver.
Select the option with the path "/run/php/php7.4-fpm.sock" and confirm.

```bash
root@DietPi:~# update-alternatives --config php-fpm.sock
There are 2 choices for the alternative php-fpm.sock (providing /run/php/php-fpm.sock).

  Selection    Path                      Priority   Status
------------------------------------------------------------
* 0            /run/php/php8.1-fpm.sock   81        auto mode
  1            /run/php/php7.4-fpm.sock   74        manual mode
  2            /run/php/php8.1-fpm.sock   81        manual mode

Press <enter> to keep the current choice[*], or type selection number:1
```

Then reload lighttpd:
```bash
service lighttpd force-reload
```

Now run the command `update-alternatives --config php` to select which PHP version should be used for the command line.
Select the option with the path "/usr/bin/php7.4" and confirm.
```bash
root@DietPi:~# update-alternatives --config php
There are 2 choices for the alternative php (providing /usr/bin/php).

  Selection    Path             Priority   Status
------------------------------------------------------------
* 0            /usr/bin/php8.1   81        auto mode
  1            /usr/bin/php7.4   74        manual mode
  2            /usr/bin/php8.1   81        manual mode

Press <enter> to keep the current choice[*], or type selection number:1
```