## Built-In Handbook
See [user handbook](./User-Handbook).


## Deleting Users
When a user gets deleted, all his data will be permanently removed with the next execution of the cron jobs.
The value of the `Remove deleted objects from database` setting will be ignored and the data will be deleted permanently.
While a user is queued for complete removal, you can not reassign the username.


## Sharing Passwords
Shared passwords are synchronized using a background job.
This means that creating, updating or deleting a shared password will not be completed until the background job has been executed.
If you want to speed up this process, we recommend running the background jobs more often.
We also strongly recommend using cron instead of webcron or ajax.
Ajax and webcron will only execute one background job at a time which will cause long delays when sharing a password.

## Repairing the Database
Passwords offers a repair job which can fix database inconsistencies like orphaned revisions or broken relations between entities.
It will also perform upgrades of entities when a new field is added or changed.
To execute the repair job, execute the Nextcloud maintenance command from the nextcloud folder `./occ maintenance:repair`

## How do i make the app look like in the app store?
- We use **Besticon** as **Favicon Service**. We recommend hosting it your self as [docker image](https://hub.docker.com/r/matthiasluedtke/iconserver/) or for free on [Heroku](https://dashboard.heroku.com/new?button-url=https%3A%2F%2Fgithub.com%2Fmat%2Fbesticon&template=https%3A%2F%2Fgithub.com%2Fmat%2Fbesticon)
- We use **Pageres** as **Website Preview Service**