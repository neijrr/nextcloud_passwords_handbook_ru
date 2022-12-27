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
# Install PHP 8.1
apt-get -y install php8.1-fpm php8.1-apcu php8.1-mysql php8.1-xml php8.1-zip php8.1-mbstring php8.1-gd php8.1-curl php8.1-redis php8.1-intl php8.1-bcmath php8.1-gmp php8.1-imagick imagemagick
```



## Update the PHP 8.1 configuration
Execute the following command on your DietPi to link the DietPi configuration for PHP from PHP 7.4 to 8.1 and enable it:
```bash
# Enable the image magick module
phpenmod imagick

# Symlink NCP PHP configuration
ln -s /etc/php/7.4/mods-available/dietpi-nextcloud.ini /etc/php/8.1/mods-available/dietpi-nextcloud.ini
ln -s /etc/php/7.4/mods-available/dietpi.ini /etc/php/8.1/mods-available/dietpi.ini
phpenmod dietpi
phpenmod dietpi-nextcloud

# Restart PHP
service php8.1-fpm restart
```

Now you need to edit the configuration of PHP FPM.
Run the command `nano /etc/php/8.1/fpm/php.ini` to open a text editor with the config file.
Find the line `;cgi.fix_pathinfo=1` and remove the `;` at the beginning so that the line reads `cgi.fix_pathinfo=1`.

You can use `CTRL` + `w` to search in the file, 
with `CRTL` + `o` you can save the changed file and 
with `CRTL` + `x` you can close the editor.



## Set up Lighttpd for PHP 8.1
Now you need to edit the configuration for lighttpd to instruct it to use PHP 8.1
Run `nano /etc/lighttpd/conf-available/15-fastcgi-php.conf` to open the configuration file.

It should have this section:
```
fastcgi.server += ( ".php" =>
        ((
                "socket" => "/run/php/php7.4-fpm.sock",
                "broken-scriptfilename" => "enable"
        ))
)
```

You need to change the "socket" from "/run/php/php7.4-fpm.sock" to "/run/php/php8.1-fpm.sock".
The section should now read like this:
```
fastcgi.server += ( ".php" =>
        ((
                "socket" => "/run/php/php8.1-fpm.sock",
                "broken-scriptfilename" => "enable"
        ))
)
```
Save the file and then run the following command to restart lighttpd:
```bash
service lighttpd force-reload
```



## Check for Nextcloud and App updates
```bash
# Check for updates
ncc update:check

# Install updates of the passwords app if available
ncc app:update passwords
```


## Check the PHP default version
By default, your DietPi should now be using PHP 8.1.
You can check this by running `php -v`. The output should look like this:
```bash
root@DietPi:~# php -v
PHP 8.1.0 (cli) (built: Mar  5 2021 08:38:30) ( NTS )
Copyright (c) The PHP Group
Zend Engine v4.0.3, Copyright (c) Zend Technologies
    with Zend OPcache v8.1.3, Copyright (c), by Zend Technologies
```

If it doesn't, you should use `update-alternatives --config php` and set PHP 8.1 as default:
```bash
root@DietPi:~# update-alternatives --config php
There are 2 choices for the alternative php (providing /usr/bin/php).

  Selection    Path             Priority   Status
------------------------------------------------------------
* 0            /usr/bin/php8.1   81        auto mode
  1            /usr/bin/php8.1   80        manual mode
  2            /usr/bin/php8.1   81        manual mode

Press <enter> to keep the current choice[*], or type selection number:0
```

## Notes
- It can take a day before app updates show up in the apps store