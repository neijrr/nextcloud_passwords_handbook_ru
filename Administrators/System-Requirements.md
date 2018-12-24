|  | Minimum | Recommended |
| --- | --- | --- |
| Processor | 2x1 GHz      | 4x2GHz |
| Ram       | 512 MiB      | 8GiB |
| Disk      | 4 GiB        | 64GiB |
| Platform  | Nextcloud 12 | Nextcloud 14 |
| OS        | Linux        | Ubuntu 18.04 |
| Database  | Sqlite / MySQL / PostgreSQL | MariaDB 10.2 |
| PHP       | PHP 7.1 | PHP 7.2 |
| Webserver | HTTPS   | Nginx 1.12.2 HTTPS |
| PECL      | Curl    | Zip, Imagick, Curl |
| Libraries |         | imagemagick, librsvg, wbritish, wamerican, wngerman, wfrench, wspanish, witalian, wportuguese |

### Version scheme and minimum requirements
Passwords versions are simply the date of the release of the version.
The exact version scheme is `<year>.<month>.<bugfix>`.
In accordance with [SemVer2.0.0](https://semver.org/spec/v2.0.0.html), backwards compatibility breaks will be introduced in the first version of a new year.
This includes the removal of support for any Nextcloud version but the latest as well as any PHP version without [active support](http://php.net/supported-versions.php).

### HTTPS
Passwords requires HTTPS to work. This can not be disabled.
Please take a look at the [Nextcloud documentation](https://docs.nextcloud.com/server/14/admin_manual/configuration_server/harden_server.html#use-https) to configure your server correctly.
You can get a free HTTPS certificate from [Let's Encrypt](https://letsencrypt.org/getting-started/).

### Background Jobs
Passwords uses several background jobs to process data.
To ensure that these run as intended, it is recommended to configure Nextcloud to run those jobs trough cron.
Using webcron or ajax for background jobs will cause long delays when passwords are shared since these options will only execute one background job with each call.
Using ajax for background jobs may also cause unexpected issues since this will execute background jobs in the user scope instead of the global scope.
More information can be found in the [documentation](https://docs.nextcloud.com/server/14/go.php?to=admin-background-jobs).

### Browser Support
The web interface of Passwords is designed to support the latest versions of major browsers.
This includes most browsers based on Chromium and Firefox Quantum (Version 57+).

### PHP Requirements
To keep your PHP version updated, we recommend the [PHP PPA from deb.sury.org](https://deb.sury.org/#php-packages)
You can install the latest version from the PPA with the following commands:
```bash
sudo add-apt-repository ppa:ondrej/php
sudo apt-get update
sudo apt-get upgrade
```

### Pageres dependencies
- PhantomJS 
- NPM 
- fontconfig

### Third Party Services
To provide all api features, passwords may use third party services depending on the settings.
The following list contains all domains which may provide these services.
However some local service providers like WKHTML, Pageres and the favicon finder may contact any domain as requested via the api.

- https://github.com
- https://passwords-app-favicons.herokuapp.com
- http://favicongrabber.com/
- https://icons.duckduckgo.com
- https://www.google.com
- https://api.screenshotapi.io
- http://api.screenshotmachine.com
- https://archive.org
- https://api.pwnedpasswords.com
- https://raw.githubusercontent.com
- http://watchout4snakes.com

### Licenses
All licensing information can be found in the [Licenses.md](https://github.com/marius-wieschollek/passwords/blob/master/Licenses.md) file