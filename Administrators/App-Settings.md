The app settings can be found in the administrative area of Nextcloud.


# Internal Data Processing
These settings influence how Passwords processes different types of data internally.

## Image Rendering
Passwords processes favicons and website previews internally for optimal performance.
The image rendering setting decides which service should be used to process images.

**Our Recommendation**: Automatic selection

| **Service**     | Automatic selection                                             | Imagick/GMagick                                                 | Imaginary                                                                                                                                                                                                                          | GDLib                                                                                                        |
|-----------------|-----------------------------------------------------------------|-----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------|
| **Description** | Automatically selects the best available service on your server | Uses the Imagemagick/Graphicsmagick library to process images   | Uses the [configured](https://docs.nextcloud.com/server/latest/admin_manual/configuration_server/config_sample_php_parameters.html#preview-imaginary-url) [Imaginary](https://github.com/h2non/imaginary) server to process images | Use the PHP graphics functions to process images                                                             |
| **Benefits**    | No configuration needed                                         | High quality local image processing, wide format support        | Better performance and scalability.                                                                                                                                                                                                | Shipped with PHP, always available                                                                           |
| **Downsides**   |                                                                 | Requires imagemagick and the php imagick module to be installed | Requires Imaginary server to be available and configured in Nextcloud                                                                                                                                                              | Poor performance, poor format support. Should only be chosen if the automatically selected service is broken |

**Note:** If you have Imagemagick selected, make sure that svg is supported. Otherwise, GDLib will be used in some cases.


# External Services
In this section you can configure all the third party services used by Passwords.


## Password Security Checks
This setting defines the service which is used to check if a password has been compromised.
[A full description of all services can be found here](./Services/Password-Security-Check-Services)

**Our Recommendation**: [Have I been pwned?](./Services/Password-Security-Check-Services#have-i-been-pwned)

| **Service**     | Have I been pwned?                                                                                                 | Big local database (25M passwords)                                                               | Small local database (5M passwords)                                                              | Big local database & Hibp?                                                                                                           |
|-----------------|--------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| **Description** | Uses [haveibeenpwned.com](https://haveibeenpwned.com/) to check for hundreds of millions of compromised passwords. | Downloads a static database of common compromised passwords and checks your passwords against it | Downloads a static database of common compromised passwords and checks your passwords against it | This service combines the "Have i been pwned?" and "Big local database" services.                                                    |
| **Benefits**    | Up-to-date, privacy friendly, large database                                                                       | All checks done locally, allows custom dataset, can be used offline                              | All checks done locally, does not require much space, allows custom dataset, can be used offline | Up-to-date, privacy friendly, large database, allows custom dataset, can be used offline, less requests to HIBP for common passwords |
| **Downsides**   | Requires online connection                                                                                         | Requires download & disk space, small compared to HIBP, rarely updated                           | Very small dataset, rarely updated                                                               | Requires download & Disk space                                                                                                       |
| **Details**     | [More details](./Services/Password-Security-Check-Services#have-i-been-pwned)                                      | [More details](./Services/Password-Security-Check-Services#big-local-database-25m-passwords)     | [More details](./Services/Password-Security-Check-Services#small-local-database-5m-passwords)    | [More details](./Services/Password-Security-Check-Services#big-local-database--hibp)                                                 |

## Password Generator Service
This service will be used to generate the basic words for a new password.

#### Select automatically
Selects the best fitting password generator service based on availability.

#### Leipzig Corpora Collection
This service supports english, german, french, italian, spanish, portuguese, dutch, dansk, czech and polish.
The service returns random words from a randomly selected corpora and has the largest language support.

#### Local Dictionary
Detects and uses locally installed dictionaries for english, german, french, italian, spanish and portuguese.
Actually available options depend on which dictionaries are installed on the server.

#### watchout4snakes.com
The service is only available in english.
It can provide words based on their rarity and type and is therefore a great service to generate easy to remember and secure passwords.

#### Random Characters
Generates strings of random letters.
This service has no dependencies but passwords may be hard to remember or write.


## Favicon Service
This service delivers the website favicons .
The icons are only fetched once for a domain and then stored locally.
If you change this setting, clear the favicon cache and your browser cache to see changes.

#### Local analyzer
Fetches the start page of the domain and searches for common icon tags.
This service usually finds the most icons, but also the most useless icons.

#### Besticon
Connects to a [besticon](https://github.com/mat/besticon) instance to find icons.
It usually returns the best icons and also good default icons if none is found.
If no api url is provided, our shared Besticon instance will be used.
The service can be self hosted by following our [tutorial](./Besticon-Self-Hosting).
The url for the service can be defined in the settings. Any compatible api is accepted.

#### favicongrabber.com
Is free, requires no software and delivers good icons.
There is an api request limit which means that it can be slower.

#### DuckDuckGo
Uses the icon service of the search engine.
All icons have a native resolution of 32 pixels.

#### Google
Uses the Google icon service.
It finds the least icons and they usually have a crappy resolution.
As usual with Google, there is no knowing what they do with any data collected by their service.

#### None
Always returns the fallback icon.
It is the fastest and most privacy-friendly service.


## Favicon Service Api
If you use a service with an API, you can enter the url here.
If you change this setting, clear the favicon cache and your browser cache to see changes.


## Website Preview Service
This service is used to generate previews of websites.

| **Service**     | Pageres CLI                                                          | screeenly                                                                                | Browshot                                                                                | screenshotmachine.com                                                    | screenshotlayer                                                     | None                                                     |
|-----------------|----------------------------------------------------------------------|------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------|--------------------------------------------------------------------------|---------------------------------------------------------------------|----------------------------------------------------------|
| **Description** | Uses the locally installed pageres-cli to generate website previews. | Can be used with [screeenly.com](https://secure.screeenly.com/) or a self hosted version | Uses the [browshot.com](https://browshot.com/) webservice to generate website previews. | Uses [screenshotmachine.com](https://screenshotmachine.com)              | Uses [screenshotlayer](https://screenshotlayer.com/)                | Delivers default images instead of previews              |
| **Benefits**    | Reliable, privacy friendly                                           | Totally free, self hosted version                                                        | Easy to use, uses real browsers, free tier                                              | Easy to use, accumulative free tier (+100 previews/month)                | Easy to use, free tier                                              | Local, privacy friendly                                  |
| **Downsides**   | Requires installing and maintaining additional software              | External service, free version no longer developed                                       | External service                                                                        | External service                                                         | External service, no HTTPS API, watermark                           | Not actually previews                                    |
| **Details**     | [More details](./Services/Website-Preview-Services#pageres-cli)      | [More details](./Services/Website-Preview-Services#screeenly)                            | [More details](./Services/Website-Preview-Services#browshot)                            | [More details](./Services/Website-Preview-Services#screenshotmachinecom) | [More details](./Services/Website-Preview-Services#screenshotlayer) | [More details](./Services/Website-Preview-Services#none) |


## Website Preview API Key
If you use "Browshot", "screenshotlayer" or "screenshotmachine.com", you will have to provide an api key here.
Otherwise, these services will not work.
If you change this setting, clear the favicon cache and your browser cache to see changes.


# Encryption Settings
Configure the encryption methods used by the app.

## Allow third party encryption
Use the configured SSEv3 user key provider for server side encryption.


# Default Email Settings
These settings can be overwritten by the user.

## Send emails for security events
Enable emails for security relevant events by default.
This will enable emails for bad passwords.

## Send emails for sharing events
Send emails when a password was shared with an user.



# Default Password Security Settings
These settings can be overwritten by the user.

## Security Check Hash
This setting defines which percentage of the SHA-1 hash used to compare each password against a list of known compromised passwords should be stored.
If your server is compromised, an attacker could use the SHA-1 hash to find the plain text value of a compromised password.
Storing a partial hash can reduce this risk, but also means that passwords may be marked as compromised despite being secure.
Storing no hash will prevent the password security check and the duplicate check from working.

Changes in this setting will be applied to new passwords immediately.
If a shorter value is selected, the hashes of existing passwords will be updated with the next password security check.
If a longer value is selected, the existing hashes will *not* be updated and remain short.
Changing this setting will have no impact on the status of passwords which were already marked as compromised.


# Backup Settings
Passwords makes regular backups of the raw password database.
These backups can be used to restore the entire database or the database of a specific user.

## Backup Interval
Specifies the interval in which backups should be created automatically.
The default value is `Every Day`.
You can also create backups manually with the command line command.

**Note:** You can not disable automated backups since we _really_ can't help you when you loose your data.

## Amount of backups to keep
Specifies the amount of backups to keep.
If the maximum is reached, the oldest backup will be deleted.
This setting also includes manually created backups.
The default value is `14`, setting the value to `0` will keep all backups.
The shorter your backup interval is, the higher this setting should be to cover at least two weeks.



# Other Settings

## Remove deleted objects from database
Specifies the time after which passwords, folders and tags deleted by the user will be removed from the database permanently.
This setting does not affect the data of deleted users which will always be deleted permanently.

## Show Nightly Updates in "Apps"
This setting will modify the Nextcloud core to enable the installation of nightly updates for the passwords app.

## Server survey participation
The server survey will send us some anonymous data of your server once a week.
This helps us to plan the future development of the app.
You can either contribute basic data (Nextcloud, App and PHP version) or full data (App Settings, Encryption usage) or no data at all.
You can read more about this [here](./Server-Survey) or take a look at our [statistics](https://statistics.passwordsapp.org/) generated from the data. 


# Caches
Caches are used to store temporary data. they are usually not emptied by the app.
If problems occur, the first tip is always to empty the related cache.

## Default Cache
Usually not used. Contains general files.

## Avatars Cache
Contains rendered images of user avatars.

## Favicon Cache
Contains the raw and scaled favicons.
This cache can not be cleared if you are using the shared BestIcon instance.

## Pageshot Cache
Contains the raw website screenshots and resized or cropped versions.

## Passwords Cache
Contains lists with bad passwords.



# Optimal settings
Which settings are optimal for you is dependent on your use case is dependent on your use case.
This table is intended to help with that choice.

| Sevice                      | Recommended                                             | Privacy friendly                                                                                                        | Offline                                                                                                                                                     |
|-----------------------------|---------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                             | Recommended services for best user experience           | Services with the least change of user data sent to others                                                              | Services which don't require internet connection                                                                                                            |
| Password Security Check     | "Hibp?" and "Big local database & Hibp?"                | "Big local database & Hibp?"                                                                                            | "Big local database" and "Small local database" with [self generated dataset](./Services/Password-Security-Check-Services#big-local-database-25m-passwords) |
| Password Generator Service  | "Select automatically" and "Leipzig Corpora Collection" | "Local dictionary" and "Random characters"                                                                              | "Local dictionary" and "Random characters"                                                                                                                  |
| Favicon Service             | "Besticon"                                              | "Besticon" ([self hosted](./Besticon-Self-Hosting)) and "Local analyzer"                                                | "None"                                                                                                                                                      |
| Website Preview Service     | "screeenly" and "Pageres CLI"                           | "Pageres CLI" and "screeenly" ([self hosted](https://github.com/stefanzweifel/screeenly/wiki/Requirements-and-Install)) | "None"                                                                                                                                                      |
| Server survey participation | "Full"                                                  | "Basic"                                                                                                                 | "None"                                                                                                                                                      |
| Other settings              | -                                                       | Install the [Passwords Handbook app](https://apps.nextcloud.com/apps/passwords_handbook)                                | Install the [Passwords Handbook app](https://apps.nextcloud.com/apps/passwords_handbook)                                                                    |