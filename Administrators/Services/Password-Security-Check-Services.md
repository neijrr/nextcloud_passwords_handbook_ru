The password app regularly checks user passwords against a database of breached passwords.
Which database this is, can be configured through the password security check service in the app settings.

### Have i been pwned?
[haveibeenpwned.com](https://haveibeenpwned.com/) hosts a large database with hundreds of millions of compromised credentials.
Their database receives regular updates with lists of leaked passwords which are usually used by hackers who to attempt to break into accounts.
They provide an api which the passwords app can use.
The api uses [k-anonymity api](https://www.troyhunt.com/ive-just-launched-pwned-passwords-version-2/#cloudflareprivacyandkanonymity) so the passwords app downloads a subset of breached passwords and compares the hashes locally.
This preserves the privacy of the passwords stored in the app as no SHA-1 hash of any password is ever sent to the api.

"Have i been pwned?" is the recommended default service for security checks as it provides up-to-date data.

##### Configuring the api url
It is possible to use a compatible api instead of the the official Hibp? api.
For this, the config key `passwords/hibp/url` needs to be set to the url of the api.
The url should contain the placeholder `:range` which will be replaced with the first five characters of the SHA-1 hash which should be checked.
The url should look like this in the end: `https://api.pwnedpasswords.com/range/:range`.

The app expects a list of matching hashes as response, with one entry per line and `\n` as line break.


### Big local database (25M passwords)
This service downloads a database with the 25 million most common passwords of the [Hibp? dataset](https://haveibeenpwned.com/Passwords) from [breached.passwordsapp.org](httsp://breached.passwordsapp.org) and installs it locally.
After the database has been downloaded, all checks are done locally. 
Which version of the dataset is downloaded is hardcoded into the app.
This means that a new version of the database is only downloaded after the app has been updated and old apps may download an outdated database.

##### Generating the database
The app offers an option to generate the password database from the source files provided by Hibp?.
In order to process the file, your server should have at least 3 GiB RAM for PHP applications and around 60 GiB of disk space.

1. Go to [Hibp?](https://haveibeenpwned.com/Passwords) and download the "Pwned Passwords list" in the SHA-1 format ordered by prevalence.
2. Unpack the archive
3. Place the file on the server and ensure it is readable by the webserver user.
4. Log into the command line of your server and navigate to the root folder of your Nextcloud installation.
5. Now run the command `php ./occ passwords:pwned-list:process <file> --size <size> --import` where `<file>` is the location to your file and `<size>` is the number of passwords to import in millions (e.g. 25).
    The option `--import` will automatically import the resulting file into the passwords app.
    When choosing the `<size>`, be aware that a greater size will also require more RAM.
6. Now place the generated ZIP-file on a location that is accessible via https and configure the database url for the service as described below.
    Even if you used the import option, the app may download the database again if the cache is cleared or a new version is released.

##### Configuring the database url
It is possible to configure a custom url for the database.
For this, the config key `passwords/hibp/url` needs to be set to the url of the api.
The url should contain the placeholders `:format` for the format of the database ("json" or "gzip") and `:version` for the version of the database used by the app.
The url should look like this in the end: `https://breached.passwordsapp.org/databases/25-million-v:version-:format.zip`.



### Small local database (5M passwords)
This service is exactly the same as the [Big local database (25M passwords)](#big-local-database-25m-passwords) service, just with a smaller database.
The service downloads a database with the 5 million most common passwords of the [Hibp? dataset](https://haveibeenpwned.com/Passwords) from [breached.passwordsapp.org](httsp://breached.passwordsapp.org) and installs it locally.
After the database has been downloaded, all checks are done locally.
Which version of the dataset is downloaded is hardcoded into the app.
This means that a new version of the database is only downloaded after the app has been updated and old apps may download an outdated database.

_This service supports the same customisation options as the [Big local database (25M passwords)](#big-local-database-25m-passwords) service_



### Big local database & Hibp?
This service combines the [Have i been pwned?](#have-i-been-pwned) service and the [Big local database (25M passwords)](#big-local-database-25m-passwords) service.
For any given SHA-1 check, the service will first compare it to the locally installed "big local database".
Only if the hash can not be found locally, it will be checked against the Hibp? api.
This improves the privacy of your users since no request to an external api is made in case they used a common insecure password.

In theory, Hibp? (or whoever runs the configured api) could record your requests against that api and then assume you were looking for the most common hash in the requested subset of hashes.
With that knowledge and the original list of passwords from which the hashes were generated, the api provider could guess a password looked up by your server if it's common.
By having a large list of common passwords locally, this scenario is prevented since no request to the api is made for the SHA-1 hash of any common password.

_This service supports all customisation options of the [Have i been pwned?](#have-i-been-pwned) service and the [Big local database (25M passwords)](#big-local-database-25m-passwords) service_