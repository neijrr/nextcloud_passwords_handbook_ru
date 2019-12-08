|  | Minimum | Recommended |
| --- | --- | --- | --- |
| Processor | 2x1 GHz                     | 4x2 GHz |
| Ram       | 512 MiB                     | 8 GiB |
| Disk      | 4 GiB                       | 64 GiB |
| Platform  | Nextcloud 17                | Nextcloud 17 |
| OS        | Linux                       | Ubuntu 18.04 |
| Database  | Sqlite / MySQL / PostgreSQL | MariaDB 10.4 |
| PHP       | PHP 7.3                     | PHP 7.3 |
| Webserver | HTTPS                       | Nginx 1.17.3 HTTPS |
| PECL      | Curl                        | Zip, Imagick, Curl |
| Libraries |                             | imagemagick, librsvg, wbritish, wamerican, wngerman, wfrench, wspanish, witalian, wportuguese |

### Version scheme and minimum requirements
Passwords versions are simply the date of the release of the version.
The exact version scheme is `<year>.<month>.<bugfix>`.
In accordance with [SemVer2.0.0](https://semver.org/spec/v2.0.0.html), backwards compatibility breaks will be introduced in the first version of a new year.
This includes the removal of support for any Nextcloud version but the latest as well as any PHP version without [active support](http://php.net/supported-versions.php).

### HTTPS
Passwords requires HTTPS to work. This can not be disabled.
Please take a look at the [Nextcloud documentation](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/harden_server.html#use-https) to configure your server correctly.
If you use a proxy or separate ssl termination point, [configure your Nextcloud accordingly](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/reverse_proxy_configuration.html).
You can get a free HTTPS certificate from [Let's Encrypt](https://letsencrypt.org/getting-started/).

### Background Jobs
Passwords uses several background jobs to process data.
To ensure that these run as intended, it is recommended to configure Nextcloud to run those jobs trough cron.
Using webcron or ajax for background jobs will cause long delays when passwords are shared since these options will only execute one background job with each call.
Using ajax for background jobs may also cause unexpected issues since this will execute background jobs in the user scope instead of the global scope.
More information can be found in the [documentation](https://docs.nextcloud.com/server/latest/go.php?to=admin-background-jobs).

### Browser Support
We support the current version of Chrome and Firefox and assume that most browsers based on these will work as well.
We do not support specific browser addons.

### PHP Requirements
To keep your PHP version updated, we recommend the [PHP PPA from deb.sury.org](https://deb.sury.org/#php-packages)
You can install the latest version from the PPA with the following commands:
```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install php7.3 php-defaults
```

### Pageres dependencies
- PhantomJS 
- NPM 
- fontconfig

### Third Party Services
To provide all api features, passwords may use third party services depending on the settings.
The following list contains all domains which may provide these services.
However some local service providers like Pageres and the favicon finder may contact any domain as requested via the api.

- https://github.com
- https://passwords-app-favicons.herokuapp.com
- http://favicongrabber.com/
- https://icons.duckduckgo.com
- https://www.google.com
- https://api.browshot.com
- http://api.screenshotlayer.com
- http://api.screenshotmachine.com
- https://secure.screeenly.com
- https://archive.org
- https://api.pwnedpasswords.com
- https://raw.githubusercontent.com
- http://watchout4snakes.com
- https://ncpw.mdns.eu/

### Licenses
All licensing information can be found in the [Licenses.md](https://github.com/marius-wieschollek/passwords/blob/master/Licenses.md) file