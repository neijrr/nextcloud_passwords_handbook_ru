## Before you start
- This tutorial was developed for and tested with DietPi 7.2 on a RaspberryPI.
- This tutorial only works if you use "Apache" as webserver.
  Run `dietpi-software` and check the setting for "Webserver Preference".
- DietPi may behave differently on other systems.
- Nextcloud 21 is required _before_ upgrading to PHP 8.0.
- This does not work for DietPi Docker. You can't upgrade PHP in a Docker image.
- _Make sure to make a backup of your entire DietPi Instance (config, data, etc.) before you do this._



## Log in as Root
If you're using SSH, log in with `ssh root@<your dietpi ip>`.
If you're directly on the device, use `sudo su`



## Add PHP Package Archive
Execute the following commands on your DietPi to add the repository PHP 8.0 from [deb.sury.org](https://deb.sury.org/#php-packages):

```bash
# Add the PHP PPA from deb.sury.org
apt-get -y install apt-transport-https lsb-release ca-certificates curl
curl -sSL -o /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg
sh -c 'echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" > /etc/apt/sources.list.d/php.list'
apt-get update
```



## Install PHP 8.0
Execute the following command on your DietPi to install PHP 8.0:

```bash
# Install PHP 8.0
apt-get -y install libapache2-mod-php8.0 php8.0-apcu php8.0-mysql php8.0-xml php8.0-zip php8.0-mbstring php8.0-gd php8.0-curl php8.0-redis php8.0-intl php8.0-bcmath php8.0-gmp php8.0-imagick imagemagick
```



## Set up Apache for PHP 8.0
Execute the following commands on your DietPi to update the Apache configuration:

```bash
# Symlink NCP PHP configuration
ln -s /etc/php/7.3/mods-available/dietpi-nextcloud.ini /etc/php/8.0/mods-available/dietpi-nextcloud.ini
ln -s /etc/php/7.3/mods-available/dietpi.ini /etc/php/8.0/mods-available/dietpi.ini
phpenmod dietpi
phpenmod dietpi-nextcloud

# Configure apache for php8.0
a2dismod php7.3
a2enmod php8.0

systemctl restart apache2
```



## Check the PHP default version
By default, your DietPi should now be using PHP 8.0.
You can check this by running `php -v`. The output should look like this:
```bash
root@DietPi:/home/pi# php -v
PHP 8.0.3 (cli) (built: Mar  5 2021 08:38:30) ( NTS )
Copyright (c) The PHP Group
Zend Engine v4.0.3, Copyright (c) Zend Technologies
    with Zend OPcache v8.0.3, Copyright (c), by Zend Technologies

```

If it doesn't, you should use `update-alternatives --config php` and set PHP 8.0 as default:
```bash
root@DietPi:/home/pi# update-alternatives --config php
There are 2 choices for the alternative php (providing /usr/bin/php).

  Selection    Path             Priority   Status
------------------------------------------------------------
* 0            /usr/bin/php8.0   80        auto mode
  1            /usr/bin/php7.3   73        manual mode
  2            /usr/bin/php7.4   74        manual mode
  3            /usr/bin/php8.0   80        manual mode

Press <enter> to keep the current choice[*], or type selection number:0
```

## Notes
- It can take a day before app updates show up in the apps store