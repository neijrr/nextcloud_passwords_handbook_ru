If you are attempting to install a release of the passwords app which requires a newer version of PHP or Nextcloud than in use on your server an exception prevents the upgrade.

## Questions
#### But i have the right PHP version installed
Please note that PHP versions differ between the command line, the webserver and even different domains on your webserver.
Run `php -v` as the the user executing cron command on your server to see which version of php is in use there.
Look at the "System" section in the Nextcloud admin area to see which version of PHP is used for your webserver.

## Compatible versions
**NOTE:** The releases listed here are outdated and do not receive any support anymore!

**NOTE:** Only versions where your PHP version _and_ your Nextcloud version are listed will work on your server.

| PHP Version | Nextcloud Version | App Version | Download |
| --- | --- | --- | --- |
| 7.1 | 14, 15, 16, 17 | 2019.12.1 | [download](https://git.mdns.eu/nextcloud/passwords/-/jobs/9150/artifacts/raw/passwords.tar.gz) |
| 7.2 | 17, 18, 19, 20 | 2020.12.1 | [download](https://git.mdns.eu/nextcloud/passwords/-/jobs/10845/artifacts/raw/passwords.tar.gz) |
| 7.3 | 17, 18, 19, 20 | 2020.12.1 | [download](https://git.mdns.eu/nextcloud/passwords/-/jobs/10845/artifacts/raw/passwords.tar.gz) |

## Downgrade the app
If the previous version has already been removed from the app, you can still downgrade manually.
You need command line access or file access to the installation folder of your Nextcloud for this

#### Via the command line
1. Open the apps or custom_apps folder where the passwords app is installed
2. Remove the current version with `rm -rf passwords`
3. Download the supported version for your server with `wget <copy link of compatible version listed above>`
4. Unpack the release with `tar -xf passwords.tar.gz`
5. Open the base folder of your Nextcloud installation
6. Run `./occ upgrade`
7. Run `/occ maintenance:mode --off` if your Nextcloud is stuck in maintenance mode

#### Via file access
1. Open the apps or custom_apps folder where the passwords app is installed
2. Remove the "passwords" folder an all its contents
3. Download the supported version for your server from the lists above
4. Unpack it on your PC with `tar -xf passwords.tar.gz` or [7Zip](https://7-zip.org/)
5. Make sure that the unpacked folder contains the app files and not a second passwords folder
6. Upload the unpacked passwords folder to your apps or custom apps folder
7. If your Nextcloud is stuck in maintenance mode and you can't upgrade via the browser, remove the maintenance flag manually.
    - Open the `config` folder in the root folder of your Nextcloud installation and download the `config.php`.
    - Edit the file in a text editor and remove the line `"maintenance" => true,`.
    - Upload the changed file
8. Click the "upgrade" button in your browser