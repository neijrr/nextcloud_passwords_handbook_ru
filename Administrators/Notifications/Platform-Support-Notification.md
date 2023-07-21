## Why am i seeing this notification?
With the first release of a new year, the passwords app drops support for all major versions of Nextcloud except the latest and all PHP versions without [active support](https://php.net/supported-versions.php) by the PHP community.
For systems that use a PHP version which is still supported by Nextcloud but not by the passwords app, the Nextcloud appstore will automatically switch to the [legacy support release](../System-Requirements#lsrlegacy-support-releases).

**NOTE:** The latest version of Nextcloud can be found in their [Maintenance and Release Schedule](https://github.com/nextcloud/server/wiki/Maintenance-and-Release-Schedule).
We don't care if wherever you're getting Nextcloud from is not up-to-date.

## What does this mean?
Your server is using a version of Nextcloud or PHP that will soon no longer receive any updates for the passwords app.
You can check the currently used version of Nextcloud and PHP in the admin area of Nextcloud.
 - If your version of Nextcloud is out of date, we recommend that you upgrade to the latest version available.
 - If your version of PHP is outdated but still supported by the latest version of Nextcloud, you will likely be able to use the [legacy support release](../System-Requirements#lsrlegacy-support-releases) through the normal Nextcloud update process.

This notification is only about the passwords app and not related to Nextcloud or any other app.

## Will the passwords app stop working?
**NO**.

This change only affects future updates of the app.
The currently installed version of the app will continue to work just like it does now.

_However it might happen that some third party services used by the app will stop working at some point._
_It can also happen that apps and other tools using the passwords api will require a newer version of that api to work._
_If this happens, we will **NOT** fix it._

## Will the app stop working if i update?
**NO**

Nextcloud checks the minimum requirements before updating an app and won't advertise updates you can not install.
If a [legacy support release](../System-Requirements#lsrlegacy-support-releases) is available for your system, it will be distributed automatically through the Nextcloud appstore and you can install it as a regular update.
If you install an update manually (by uploading the new version to your server), Nextcloud will just deactivate the app.

## Why are you doing this?
Because supporting a large amount of Nextcloud releases, PHP versions and Databases also creates a large amount of possible usage scenarios.
This means that we have to spend a lot of time on testing the app with all the supported software, adding workarounds for bugs and creating slow compatibility layers to support different Nextcloud APIs.
In result, the app gets slower and is more likely to be buggy which then leads to more users requesting support from the developers.
We believe that our time is better spent developing new features than figuring out how to support dozens of Nextcloud major releases.

## What if i already use a Legacy Support Release?
The notification appears when your system does not meet the future requirements of the build that you are using.
If you see this notification while using an LSR, you will not be able to receive any further updates after support ends.

## What if i need help with my outdated version of the app?
We're happy to help you with upgrading in our [forum](https://help.nextcloud.com/c/apps/passwords) or [chat](https://t.me/nc_passwords/1).
We won't help you with issues in your outdated version of the passwords app.
We will also close any ticket on our official bugtracker if you're not using the latest version of the app.

## Where can i find the system requirements?
[Here.](../System-Requirements)
