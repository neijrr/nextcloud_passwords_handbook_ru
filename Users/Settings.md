The settings section can be found in `More > Settings`.
These settings allow you to define how the app itself and the official client behave.

[![The Settings section](_files/settings-overview.png)](_files/settings-overview.png)

## Security
### Password Generator
These settings define how the built-in password generator creates passwords.
You may be able to temporarily overwrite these settings when creating a password.
Your system administrator can choose which service is used to generate passwords.
Based on the service the actual generated password may differ.

##### Password strength
A higher password strength result in a more complex and longer password.
Every password will have at least 12 characters minimum.
With strength set to `3`, three words will be used and with `4` it will be four words.

##### Include numbers
If activated, the password generator will add numbers to the created password.

##### Include special characters
If activated, the password generator will add special characters like `$, €, @` to the created password.


## User Interface
##### Initial section
Here you can choose which section will be shown when you open the passwords app.
By default the `All Passwords` section will be shown, but you can also select your `Favourites`, `Folders`, `Tags` or `Recent` passwords as inital section.

### Password List View
These settings change how passwords are displayed in the list view.

##### Set title from
By default the name of the password will be shown in the list view.
You can also select the `Website` or the `Username` to be used.

##### Sort by
This option lets you choose which field will be used to sort passwords, when "Sort by Name" is selected in the list view.
By default the title field from the previous option will be used.
But you can also have your passwords sorted by `Name`, `Website` or `Username` independently from the title field.

##### Add copy options in menu
If this option is enabled, the `⋯`-menu will contain two menu entries to copy the password and the username.
By default these menu entries are not visible since you can copy the password by clicking on the name and the username by clicking twice.
On mobile devices the menu entries will always be shown regardless of whether this option enabled.

##### Show tags in the list view
You can show the tags for a password in the list view.
If you click on a tag the tag section will be opened and you can see all passwords with the tag.
This will increase the loading times if you have a lot of tags.
Also the tags will not be shown on mobile devices.
[![Tags in the list view](_files/tags-hover.gif)](_files/tags-hover.gif)


## Notifications
### Send Emails for
These settings enable or disable the emails sent to you by Passwords.
**Note:** Emails will only be sent if your account has an email address.

##### Security issues
Passwords checks whether your passwords are still secret or can be found in public data breaches every day.
If one or more of your passwords can be found open on the internet, Passwords will send you an email if this option is enabled.

##### Passwords shared with me
If this option is enabled, you will receive emails when someone shared a new password with you.

### Show Notifications for
##### Security issues
Passwords checks whether your passwords are still secret or can be found in public data breaches every day.
If one or more of your passwords can be found open on the internet, Passwords will show a notification if this option is enabled.
Passwords will also send a notification in any suspicious events concerning your account have been noticed.

##### Passwords shared with me
If this option is enabled, you will receive notifications when someone shared a new password with you.

##### Other errors
Tasks like sharing passwords, security checks and database housekeeping will run independently in the background.
If any errors happen during these tasks and this option is enabled, you will be notified.

## Danger Zone
The options in this section might irreversibly delete data from your account.
Therefore it is recommended that you use them with caution.

##### Reset all settings
This option will delete all settings stored in the passwords app.
This will not only reset the settings visible here, but may also include settings from other apps or browser extension using the Passwords API.
Deleted settings can not be restored.

##### Delete everything
This option will delete all passwords, folders, tags and settings in your account.
It will also delete your private encryption key. This means that your data can not be restored.
You should make a backup and confirm that the backup works before you use this option.
**Note:** This option does not reset access tokens used by third party clients.
You can delete these in your personal settings.