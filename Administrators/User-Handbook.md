Passwords features a build-in handbook to provide uses with an easy to access help whenever they need it.
This handbook is constantly updated and will therefore be always fetched directly from our [github repository](https://github.com/marius-wieschollek/passwords/wiki).
If you are running an outdated version of Passwords, the handbook may be inaccurate.
Since the handbook resources will be fetched when they are requested, the handbook domain (raw.githubusercontent.com) will be whitelisted in the Content Security Policy of the app.

## Self-Hosting the Handbook
#### Requirements
A server which can be accessed by your users without authentication and which allows requests from the domain of your Nextcloud server.

**Note:** Check your CORS setup to make sure the browser won't block requests to the handbook server.

#### Clone our wiki
The handbook is part of our wiki, therefore you should clone it if you don't want to write your own handbook from scratch.
Make sure that folders like `.git` are not accessible trough your webserver.

Clone the wiki
```bash
git clone ssh://git@git.mdns.eu:2024/nextcloud/passwords.wiki.git
cd passwords.wiki
```
The wiki is now cloned to the folder `passwords.wiki`.
The data for the user handbook is in the subfolder `Users`.

#### Update the handbook url
Use the following command to point the app to your custom handbook
```bash
./occ config:app:set passwords handbook/url --value https://yourdomain.org/path/Users
```
Passwords will try to load the file `https://yourdomain.org/path/Users/Index.md` when the handbook is opened.
If you set an invalid handbook url, the default url will be used.


## App feature management with the handbook
The app has the ability to enable/disable some features trough a file in the handbook.
Those features are usually complete in the app itself, but require changes in external services before they work.
The features available change between app versions.

To enable/disable those features, the file [`_files/deferred-activation.json`](../../Users/_files/deferred-activation.json) can be used.
The file will always be loaded when such a feature could be requested by the app.

**Note:** Enabling features which are disabled by default can cause issues and is not supported

| Scope | Feature | Description |
| --- | --- | --- |
| server | two-factor-tokens | Require 2FA tokens if available |
| server | legacy-client-warning | Show a notification if a client is using the old api |
| server | client-side-encryption | Allow users to set up client side encryption |
| webapp | encryption-tests | Test client side encryption on the user device |
| webapp | client-side-encryption | Enable client side encryption setup in the settings |
| webapp | first-run-wizard | Enable the first run wizard with CSE setup |
| webapp | backup-encryption | Enable encryption for database exports |