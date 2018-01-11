|  | Minimum | Recommended |
| --- | --- | --- |
| Processor | 4x1 GHz | 4x2GHz |
| Ram | 512 MiB | 8GiB |
| Disk | 4 GiB | 64GiB |
| Platform | Nextcloud 12 | Nextcloud 12 |
| OS | Linux | Ubuntu 16.04 |
| DB | Sqlite / MySQL / PostgreSQL | MariaDB 10.2 |
| PHP | PHP 7.1 | PHP 7.2 |
| Webserver  | HTTPS | Nginx 1.12.2 HTTPS |
| PECL | Curl | Zip, Imagick, Curl |
| Libraries | - | wbritish, wamerican, wngerman, wfrench, wspanish, witalian, wportuguese |

### Browser Support
The web interface of Passwords is designed to support the latest versions of major browsers.
This includes most browsers based on Firefox Quantum (Version 57+), Chromium and Edge.

### HTTPS
Passwords requires HTTPS to work. This can not be disabled.
Please take a look at the [Nextcloud documentation](https://docs.nextcloud.com/server/12/admin_manual/configuration_server/harden_server.html#use-https) to configure your server correctly.
You can get a free HTTPS certificate from [Let's Encrypt](https://letsencrypt.org/getting-started/).

### Wkhtml dependencies
- libmagickwand 
- libXrender1 
- libfontconfig1 
- libXext6

### Third Party Services
To provide all api features, passwords may use third party services depending on the settings.
The following list contains all domains which may provide these services.
However some local service providers like WKHTML and the favicon finder may contact any domain as requested via the api.

- https://github.com
- https://icons.better-idea.org
- https://icons.duckduckgo.com
- https://www.google.com
- https://api.screenshotapi.io
- http://api.screenshotlayer.com
- http://api.screenshotmachine.com
- https://archive.org
- https://haveibeenpwned.com
- https://raw.githubusercontent.com
- http://watchout4snakes.com

### Licenses
All licensing information can be found in the [Licenses.md](https://github.com/marius-wieschollek/passwords/blob/master/Licenses.md) file