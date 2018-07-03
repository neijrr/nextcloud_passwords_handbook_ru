## Built-In Handbook
Passwords features a build-in handbook to provide uses with an easy to access help whenever they need it.
This handbook is constantly updated and will therefore be always fetched directly from our [github repository](https://github.com/marius-wieschollek/passwords/wiki).
If you are running an outdated version of Passwords, the handbook may be inaccurate.
Since the handbook resources will be fetched when they are requested, the handbook domain (raw.githubusercontent.com) will be whitelisted in the CSP.

##### Using a custom or self hosted handbook
You can set a custom location for the handbook with the following command.
```bash
./occ config:app:set passwords handbook/url --value https://yourdomain.org/path/to/base/dir/
```
Passwords will try to load the file `https://yourdomain.org/path/to/base/dir/Index.md` when the handbook is opened.
While Passwords will take care of the Nextcloud content security policy, you will have to make sure that the CORS policy of the handbook server allows requests from your Nextcloud.
If you set an invalid handbook url, the default url will be used.


## Deleting Users
When a user gets deleted, all his data will be permanently removed with the next execution of the cron jobs.
The value of the `Remove deleted objects from database` setting will be ignored and the data will be deleted permanently.
While a user is queued for complete removal, you can not reassign the username.


## Sharing Passwords
Shared passwords are synchronized using a cron job.
This means that creating, updating or deleting a shared password will not be completed until the cron job has been executed.
If you want to speed up this process, you can run your cron jobs more often.

## Repairing the Database
Passwords offers a repair job which can fix database inconsistencies like orphaned revisions or broken relations between entities.
It will also perform upgrades of entities when a new field is added or changed.
To execute the repair job, execute the Nextcloud maintenance command from the nextcloud folder `./occ maintenance:repair`