This guide helps you to migrate fom the [Passwords Legacy](https://github.com/marius-wieschollek/passwords-legacy) app written by Fallon Turner and maintained by Marius Wieschollek.
If you did not use the legacy app or want to [start from scratch](#starting-from-scratch), this guide is not relevant for you.


### Why you should upgrade
With the release of Passwords 2018.1 at the beginning of february 2018, Passwords Legacy will only receive patches for larger security issues.
With the release of Passwords 2019.1 at the beginning of 2019, Passwords Legacy will not receive any updates at all anymore.
Passwords is more secure, faster and comes with a more powerful api and a modern webinterface.

### Prerequisites
Make sure to upgrade to the latest version of the [legacy app](https://github.com/marius-wieschollek/passwords-legacy) before attempting the migration.
Check the [system-requirements](System-Requirements.md) and make sure your server fulfills all the minimum requirements.
The migration works **only** on PHP 7.1. If you can not use PHP 7.1, perform the migration on the developer docker system and copy the databases and configuration for the app back to your productive system.
It might also be a good idea to check the issue trackers [on github](https://github.com/marius-wieschollek/passwords/issues) and [gitlab](https://git.mdns.eu/nextcloud/passwords/issues) to see if any problems with the migration process have occurred.


### Database Backup
Passwords has no write capabilities for Passwords Legacy built-in and does not use the legacy tables.
It is still a good idea to make a backup of the following tables before you start the migration process.
**Do not keep this backup in any publicly accessible folder of your webserver**

```
*PREFIX*passwords
*PREFIX*passwords_categories
*PREFIX*passwords_share
```


### Setup Testing System
We do not recommend performing the update on a live system before testing it.
If you have a staging / testing environment use it to test the migration before migrating the live system.
If you do not have a separate environment for testing, you can use the [docker setup for developers](https://git.mdns.eu/nextcloud/passwords/blob/master/CONTRIBUTING.md).
After finishing the setup, import the database dump from the previous step and set the `passwordsalt` and `secret` in the `config.php` to the same values as on your live system.
If you used password sharing in the legacy app, you should import a complete dump of your live database since the migration will not migrate shares if the user it was shared with does not exist.
Make sure to set the `installed_version` value on your testing system to `2017.12`:
```sql
UPDATE `*PREFIX*appconfig` SET `configvalue` = '2017.12' WHERE `*PREFIX*appconfig`.`appid` = 'passwords' AND `*PREFIX*appconfig`.`configkey` = 'installed_version'; 
```
Please note that the migration will check the security status of all passwords during the migration.
By default this is done with the [haveibeenpwned.com](https://haveibeenpwned.com/) web service which takes 1.5 seconds per password.
You can change this with the following sql statement:
```sql
UPDATE `*PREFIX*appconfig` SET `configvalue` = 'bigdb' WHERE `*PREFIX*appconfig`.`appid` = 'passwords' AND `*PREFIX*appconfig`.`configkey` = 'service/security'; 
```
Lastly you should know that every time you start the migration, it will try to import all categories, passwords and shares.
So in order to prevent duplicate passwords, you should empty the password tables if you have to start the migration process anew.


### Migration
Install the newest version of Passwords from the app store or the builds page.
You can also use the sources, but you will have to run `npm install` and `npm run build` to compile the files.
Nextcloud should detect the new version and activate the maintenance mode.
You can start the migration by clicking the upgrade button on the web interface or by using the command line tool.
We recommend using the command line tool for the migration.
Execute the following command in the root directory of your Nextcloud installation to use it.
```bash
./occ upgrade
```
If the migration was successful, the number of migrated passwords, categories and shares should be listed in the log.


### Post Migration Steps
- Check the Webinterface of the apps to see if any problems can be found
- If you are sure that everything works, delete the legacy tables
- After the migration, shared passwords might not be shown in the receivers account for some time. (See [known issues](#known-issues))
- If you did not use haveibeenpwned.com during the migration, the security status might be wrong for up to 24 hours. (See [known issues](#known-issues))
- Check the [known issues](#known-issues) if you encountered any problems
- Check the admin settings page


### Known Issues
###### Shared passwords are not shown
This is due to the way shares work in Passwords.
The shared passwords will be added to the receivers account by a background cron job.
If you want to speed up the process, execute the cron jobs manually
```bash
php ./cron.php
```

###### Security status of passwords is not correct
If you use one of the local databases for bad passwords, passwords might get marked as secure even if they are not.
The password databases have to be downloaded before passwords are checked correctly.
This is done by a background cron job and can take up to one day.

###### Not listed issues
If your issue is not listed here, try the [public issue tracker](https://github.com/marius-wieschollek/passwords/issues).
Please describe your issue in detail and precise and supply all necessary information to find a solution.


### Starting from scratch
If you have used passwords legacy but do not want to migrate your old data you can just disable the migration tool by setting the `installed version` to `2018.0`.
Make sure you also delete the legacy app tables from your database.
```sql
UPDATE `*PREFIX*appconfig` SET `configvalue` = '2018.0' WHERE `*PREFIX*appconfig`.`appid` = 'passwords' AND `*PREFIX*appconfig`.`configkey` = 'installed_version'; 
```