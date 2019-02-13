## Legacy Api Support
The Legacy API is the API which was originally provided by the Passwords App in versions prior to 2018.1.
This API is used by many clients for passwords and therefore still available.
However the API does not support client side encryption or safe server side encryption.
It is also makes the application slower and does not strictly enforce HTTPS.

#### Enable Legacy API
This option enables or disables the API completely.
If the API is disabled it will no longer be possible to access it in any way as the app will no longer register the necessary components in Nextcloud.

**Note:** The browser extension does not support the new api in versions prior to 2.0.0.

#### Legacy API was last used on
This settings is read only.
It should tell you when the legacy api was last used.
If you can see that the api is no longer in use on your server, you should disable it.



## Internal Data Processing
These settings influence how Passwords processes different types of data internally.

#### Image Rendering
You have two options for image rendering.
If Imagemagick or Graphicsmagick are installed on your system, they will automatically be chosen as default.
GDLib should only be chosen if Imagemagick is broken or not available.
GDLib usually provides lower image quality and might not work with all formats.

**Note:** If you have Imagemagick selected, make sure that svg is supported. Otherwise GDLib will be used in some cases.



## External Services
In this section you can configure all the third party services used by Passwords.


#### Password Security Checks
This service is used to check if a password is safe or not.

**Have I been pwned?** is the recommended service.
Is might be slow if a lot of passwords needs to be processed, since you can only make one request every 1.5 seconds.
But in general it has the largest database and is updated regularly.
If a bad password is found, the hash is stored locally so that the service does not need to be contacted again.

**10 Million Passwords** downloads a static password file and fills the local cache with it.
After this, all password checking can be done locally.
It is faster than Hibp when it comes to checking passwords, but of course it does not contain that many passwords.
Updating the database can take up to 1.75Gib of RAM or up to 125MiB on less powerful systems.
If you do not have that much ram available, you should not use this service.
It also requires up to 512Mib of disk space.

**1 Million Passwords** downloads a static file with the most common passwords.
It uses a lot less system resources than the 10Mio passwords and should run on any system.

**10 Mio Passwords + Have I been pwned?** fills the local cache with the most common passwords.
It is faster if a bad password is found in the 10 Mio Passwords database since Hibp is not contacted in that case.


#### Password Generator Service
This service will be used to generate the basic words for a new password.

**Local Dictionary** uses locally installed dictionaries for different languages to provide words.
It has the best language support.

**watchout4snakes.com** is only available in english.
It can provide words based on their rarity and type and is therefore the best service to generate easy to remember and secure passwords.

**Random Characters** generates sets of random letters for the service.
This service has no dependencies.


#### Favicon Service
This service delivers the website favicons .
The icons are only fetched once for a domain and then stored locally.

**Local analyzer** fetches the start page of the domain and searches for common icon tags.
This service usually finds the most icons, but also the most useless icons.

**Besticon** uses a [besticon](https://github.com/mat/besticon) third party service to find icons.
The service can be self hosted by using the [docker image](https://hub.docker.com/r/matthiasluedtke/iconserver/), fore free on [Heroku](https://dashboard.heroku.com/new?button-url=https%3A%2F%2Fgithub.com%2Fmat%2Fbesticon&template=https%3A%2F%2Fgithub.com%2Fmat%2Fbesticon) or running the app on a server.
The url for the service can be defined in the settings. Any compatible api is accepted.
It usually returns the best icons and also good default icons if none is found.

**DuckDuckGo** uses the icon service of the search engine.
All icons have a native resolution of 32 pixels.

**Google** uses googles icon service.
It finds the least icons and they usually have a crappy resolution.

**None** always returns a default icon.
It is the fastest and most privacy friendly service.


#### Favicon Service Api
If you use a service with an API, you can enter the url here.
The default url for the besticon service is https://passwords-app-favicons.herokuapp.com/icon.


#### Website Preview Service
This service is used to generate previews of websites.
Only the front page of the domain is called and at maximum twice for mobile and desktop views.
If you know a good program or service, feel free to open an issue to support it.
(Requirements: Offers a free plan and has an api)

**Pageres/PhantomJS** requires pageres-cli and phantomJS to installed locally.
Usually very reliable local and headless preview generator with a modern browser engine.
If the installation with NPM fails, try `sudo npm install --global pageres-cli@4.1.0 --unsafe-perm`.

**screenshotapi.io** offers a huge amount of free screenshots, uses HTTPS and is generally very cheap.
It might be slower and sometimes crashes.

**screenshotmachine.com** offers 100 fresh screenshots for free per month and impressions are free.
You only have to pay what you use and it is quite fast and supports different devices.
For free accounts, HTTPS is not supported.

**None** just delivers one of five default images.


#### Website Preview API Key
If you use a service with an api, you have to put your api key here.



## Default Email Settings
These settigns can be overwritten by the user.

#### Send emails for security events
Enable emails for security relevant events by default.
This will enable emails for bad passwords.

#### Send emails for sharing events
Send emails when a password was shared with an user.



## Backup Settings
Passwords makes regular backups of the raw password database.
These backups can be used to restore the entire database or the database of a specific user.

#### Backup Interval
Specifies the interval in which backups should be created automatically.
The default value is `Every Day`.
You can also create backups manually with the command line command.

**Note:** You can not disable automated backups since we _really_ can't help you when you loose your data.

#### Amount of backups to keep
Specifies the amount of backups to keep.
If the maximum is reached, the oldest backup will be deleted.
This setting also includes manually created backups.
The default value is `14`, setting the value to `0` will keep all backups.
The shorter your backup interval is, the higher this setting should be to cover at least two weeks.



## Other Settings

#### Remove deleted objects from database
Specifies the time after which passwords, folders and tags deleted by the user will be removed from the database permanently.
This setting does not affect the data of deleted users which will always be deleted permanently.

#### Enable Passwords Nightly Builds
This setting will modify the Nextcloud core to enable the installation of nightly updates.
The system config key `allowNightlyUpdates` will contain an array of apps for which the nightly updates are enabled.

**Note:** You can add other apps to `allowNightlyUpdates` or remove passwords from it manually, but the functionality will only work if the backend option is enabled.


## Caches
Caches are used to store temporary data. they are usually not emptied by the app.
If problems occur, the first tip is always to empty the related cache.

#### Default Cache
Usually not used. Contains general files.

#### Avatars Cache
Contains rendered images of user avatars.

#### Favicon Cache
Contains the raw and scaled favicons.
This cache can not be cleared if you are using the shared BestIcon instance.

#### Pageshot Cache
Contains the raw website screenshots and resized or cropped versions.

#### Passwords Cache
Contains lists with bad passwords.