## Why am i seeing this notification?
With the first release of a new year, the passwords app drops support for all major versions of Nextcloud except the latest and all PHP versions without [active support](https://php.net/supported-versions.php) by the PHP community.
Around half a year before this, the admin settings of the app will show a warning if the server runs on an old software platform.
Three months before the end of support, each update creates a notification reminding administrators to update.
This should give administrators enough time to plan and execute any necessary updates.

**NOTE:** Since the "current" version of Nextcloud can vary based on where you get updates from, we define the latest stable version as the version listed on the [Nextcloud download page](https://nextcloud.com/install/#instructions-server).

## What does this mean?
Your server is using a version of Nextcloud or PHP that will soon no longer receive any updates for the passwords app.
We recommend that you check the installed version of Nextcloud and PHP in the admin area and upgrade them if necessary.
This notification is only about the passwords app and not related to Nextcloud or any other app.

## Will the passwords app stop working?
**NO**.

This change only affects future updates of the app.
The currently installed version of the app will continue to work just like it does now.

_However it might happen that some third party services used by the app will stop working over time._
_It can also happen that apps and other tools using the passwords api will require a newer version of that api to work._
_If this happens, we will **NOT** fix it._

## Will the app stop working if i update?
**NO**

Nextcloud will check the minimum requirements before updating an app and won't advertise updates you can not install.
Any update shown in the app store can be installed, even if your server does not meet our minimum requirements of the latest version of passwords.
If you install an update manually (by uploading the new version to your server), Nextcloud will just deactivate the app.

## Why are you doing this?
Because supporting a large amount of Nextcloud releases, PHP versions and Databases also creates a large amount of possible usage scenarios.
This means that we have to spend a lot of time on testing the app with all the supported software, adding workarounds for bugs and creating slow compatibility layers to support different Nextcloud APIs.
In result, the app gets slower and is more likely to be buggy which then leads to more users requesting support from the developers.
We believe that our time is better spent developing new features than figuring out how to support dozens of Nextcloud major releases.

## What if i need help with my outdated version of the app?
We're happy to help you with upgrading in our [forum](https://help.nextcloud.com/c/apps/passwords) or [chat](https://t.me/nc_passwords).
We won't help you with issues in your outdated version of the passwords app.
We will also close any ticket on our official bugtracker if you're not using the latest version of the app.

## Where can i find the system requirements?
[Here.](../System-Requirements)
