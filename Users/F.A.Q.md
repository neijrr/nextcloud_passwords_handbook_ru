## General
#### Error "Your Browser is outdated"
If your browser does not support the necessary APIs used by Passwords, you will see this message.
This means that your browser does not provide some functionality which is absolutely required to run the app.
Passwords checks the existence of such functionality and shows the message only if it is not present.
You may use a known working browser like Firefox or Vivaldi to run the app.

**NOTE:** Please do not ask us to "make your browser compatible". If we could, you would not see this message.

#### Error "HTTPS Required"
This error appears if you tried to open the app with an unsecure connection.
Using Passwords via HTTP is not only insecure, the app will also not work.
You can solve this issue by prefixing the url with `https://<your nextcloud url>`.
If the server does not support HTTPS, this error can not be solved.

#### Can i access passwords offline?
**No.** A connection to the Nextcloud server is always required to access passwords.


## Security
#### How secure is Passwords?
How secure your passwords are with the Passwords app depends on two main factors.
_You are one of it._

- Enable our [end to end encryption for your passwords](./Encryption/Enable-End-to-End-Encryption)
- Make sure to keep your Nextcloud account safe.
- Only access the cloud over HTTPS and do not give your credentials to someone else.
- Do not log into Nextcloud on someone else's pc or a public pc.
- If you are using a client to access your passwords, make sure it is always up-to-date.

The second main factor is the administrator of your Nextcloud instance.

Any security issues in Nextcloud, other Nextcloud apps and the server in general is also a security issue for the Passwords app.
So in order to keep your passwords safe, your server administrator has to keep the server safe.

A bad administrator could also manipulate Nextcloud in a way to steal your passwords even when client side encryption is enabled.
So you will have to trust your administrator to keep the server safe.



#### I got the notification "Suspicious amount of failed login attempts detected"
The Passwords app counts failed attempts to unlock the password database with the master password.
If five failed login attempts are detected, the app will revoke the app password the client that made the attempt.
After that, the app will also revoke the app password of any other client after one failed login attempt by that client.
The app will also prevent any client not using an app password from accessing the app at all.
This means that clients which use your Nextcloud username and password to access the passwords app will not be able to even attempt to log in.
All restrictions will be lifted as soon as you unlock the password database in with the correct mater password.
However even after the restrictions are lifted, you will have to create a new app password for any client that had its app password revoked before.

#### What does the Passwords Session Token do?
When you use the Passwords app, tokens with the naming schema "Passwords Session MM.DD.YY HH:MM - User@IP Address" will appear in your device & sessions list.
These tokens are generated automatically when you access the Passwords app in Nextcloud.
The tokens are only valid for a short period of time and usually do not have file system access.
It is safe to delete the tokens, but you should be aware that this will close currently open sessions.

#### How do i create a master password?
Take a look at [the guide to enable end-to-end encryption](Encryption/Enable-End-to-End-Encryption).
Open the Settings (`More > Settings`) and look for the "Encryption" section.
Enable the client-side encryption option and set an encryption passphrase.

**Note:** This can not be undone. You can change the master password but not remove it.

#### How do i use two factor authentication (2FA)?
If your Nextcloud account is set up to use 2FA, the app will automatically require it if the feature is enabled.
If you have 2FA set up, but the app does not require it on login, please ask yor admin to enable two factor authentication.

**Note:** Some third party clients do not support 2FA and will be unusable after enabling it.


## Sharing
#### I have shared / unshared a password, but the other person can not / still see it
Passwords permits users to access the data of other users themselves.
Because of this, changes in shared passwords need to be processed by a privileged automated process on the server.
This is usually done every 15 minutes.
This process will always execute changes made by the original owner first and discard the changes of others if there is any conflict.

#### Some of my shares show a loading that says "Some data is waiting to be synchronized"
As described in the [question above](#i-have-shared-unshared-a-password-but-the-other-person-can-not-still-see-it), shared passwords are synchronized in the background.
So if you or someone else changes the shared password, it is queued for synchronizing.
Until all changes have been synchronized, the loading animation will tell you that changes are waiting to be synchronized.

#### What happens if I delete a password that was shared with me?
If you delete a password that was shared with you, it will only be deleted from your account and the accounts of the people you may have shared the password with.
Even if you have the rights to edit the password, you can not delete it in the account of the person who shared it with you.


## Import and Export
#### I want to import from another password manager but there is no option for this service
Most password managers do offer a CSV export.
If you have that csv file, you can choose the option "Other / Custom CSV" and map the fields yourself.
See the [custom CSV import guide](./Import/Import-from-custom-CSV) for further information.

#### A warning says that the service i am trying to import from is known to generate faulty csv files
Some password services create export files where the columns are not formatted properly.
If that happens, Passwords may be unable to import the file as it is and you have to fix it manually.
See the [import section](./Import#how-to-fix-faulty-csv-files) for further information.


## Performance
#### The app is slow after failed logins
If you repeatedly tried to login with any third party client using incorrect login data, Nextcloud will see this as a brute force attack.
This results in a slowdown of any further api requests.
Since the app uses the api, this slowdown will also affect it.
The normal performance should be restored after some time.

#### The "All" section or folders with many items are slow
All passwords, folders and tags are stored encrypted and decrypting can take up considerable amounts of time.
The generation of favicons for each password can also take some time initially.
Using folders or tags to organize and browse your passwords will increase performance.


## Notifications and Emails
#### Passwords tells me that one of my passwords is insecure
If companies get hacked, the passwords of their users often end up in online databases of hacked passwords.
Because of this, the passwords app checks on a regular basis if one of your passwords appears in these databases and notifies you if it does.
This does not necessarily mean that you or the website which you use the password for have been hacked.
But you should change the password as hackers now have it in their databases as well.
You can view all your insecure passwords in `Security > Broken`.

#### Password tells me that one of my passwords could not be shared
Given that the option is enabled, you can share passwords which have been shared with you.
By doing so, it might happen that the person you want to share the password with, is the one who originally shared it.
If that is the case, Passwords will not complete the sharing process as this would create an endless loop.
You can view all your shared passwords in `Shared > Shared by me`.

#### The notification "We have detected several failed attempts to unlock your password database by ..."
If you use 2FA or a master password, the app will send you a notification if a client tries to gain access to the database without correct credentials.
If this was not you, we recommend revoking the app password of that client in the "Security" section of your Nextcloud account settings.
If the client was not using an app password, we recommend that you change your account password and delete all the app passwords (Changing your password will invalidate the app passwords).

#### The notification "Administrative access to your account"
An administrator has opened the passwords app with your account trough an app like [impersonate](https://apps.nextcloud.com/apps/impersonate).
If you use a master password, then this does not necessarily mean that access to your passwords was possible.
For more information please talk to your administrator.

#### The notification "Legacy API: Time to say goodbye!"
You are still using third party software that accesses the passwords trough the old api from ocPasswords.
This is not recommended and will cause issues if you use client side encryption.
It is recommended that you update that client or look for a replacement.