> This page contains the system requirements for the [passwords app for Nextcloud](https://apps.nextcloud.com/apps/passwords).
> If you're looking for the Nextcloud server system requirements [click here](https://docs.nextcloud.com/server/latest/admin_manual/installation/system_requirements.html).

|  | Minimum | Recommended |
| --- | --- | --- |
| Processor | 2x1 GHz                     | 4x2 GHz |
| Ram       | 512 MiB                     | 8 GiB |
| Disk      | 4 GiB                       | 64 GiB |
| Platform  | Nextcloud 20.0.5            | Nextcloud 20.0.5 |
| OS        | Linux                       | Ubuntu 20.04 |
| Database  | Sqlite / MySQL / PostgreSQL | MariaDB 10.5 |
| PHP       | PHP 7.4                     | PHP 7.4 |
| Webserver | HTTPS                       | Nginx 1.19 HTTPS |
| PECL      |                             | Zip, Imagick |
| Libraries |                             | imagemagick, librsvg, wbritish, wamerican, wngerman, wfrench, wspanish, witalian, wportuguese |

### Version scheme and breaking changes
Passwords versions are simply the year and month of the release of the version.
The exact version scheme is `<year>.<month>.<bugfix>`.
In accordance with [SemVer2.0.0](https://semver.org/spec/v2.0.0.html), only the first version of a new year will introduce breaks in backward compatibility.
With the first release of the year, the support for any Nextcloud version but the latest as well as any PHP version without [active support](https://php.net/supported-versions.php) will be ended.

### HTTPS requirement
Passwords requires HTTPS to work. This can not be disabled.
Please take a look at the [Nextcloud documentation](https://docs.nextcloud.com/server/latest/admin_manual/installation/harden_server.html#use-https-label) to configure your server correctly.
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
We do not support specific configurations or browser extensions.

### PHP Requirements
We support **only** versions of PHP with **[active support](https://php.net/supported-versions.php)** by the PHP community.
The app may run with older PHP versions but this is not tested and bug reports with an unsupported version will be ignored.

To keep your PHP version updated, we recommend the [PHP PPA from deb.sury.org](https://deb.sury.org/#php-packages) for Ubuntu and Debian.
If you use NextcloudPi, you can use our [NextcloudPi PHP 7.4 ugprade guide](./Guides/NextcloudPi/Upgrade-to-PHP-7.4).

### Pageres dependencies
- NPM 
- fontconfig

### Third Party Services
To provide all api features, passwords may use third party services depending on the settings.
The following list contains all domains which may provide these services.
However some local service providers like Pageres and the favicon finder may contact any domain as requested via the api.
The [user handbook](./User-Handbook) also makes direct requests to external servers from the user browser and your server.

- https://github.com
- https://ncpw-besticon-01.herokuapp.com
- https://ncpw-besticon-02.herokuapp.com
- https://favicongrabber.com/
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
- http://api.corpora.uni-leipzig.de
- https://ncpw.mdns.eu

### Licenses
All licensing information can be found in the [Licenses.md](https://github.com/marius-wieschollek/passwords/blob/master/Licenses.md) file