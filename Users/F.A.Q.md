## Security
#### I found a strange WebUi Device Token
When you use the Passwords app, a token called "Passwords WebUI Access" will appear in your device list.
This token was automatically generated to enable the app to access your passwords.
There should only be one token with this name and it should not have filesystem access.
If you don't use Passwords or the token appears more than once, you should delete it. 


## Sharing
#### I have shared / unshared a password, but the other person can not / still see it
Passwords permits users to access the data of other users themselves.
Because of this, changes in shared passwords need to be processed by a privileged automated process on the server.
This is usually done every 15 minutes.
This process will always execute changes made by the original owner first and discard the changes of others if there is any conflict.

#### What happens if I delete a password that was shared with me?
If you delete a password that was shared with you, it will only be deleted from your account and the accounts of the people you may have shared the password with.
Even if you have the rights to edit the password, you can not delete it in the account of the person who shared it with you.


## Notifications
#### Passwords tells me taht one of my passwords is insecure
If companies get hacked, the passwords of their users often end up in online databases of hacked passwords.
Because of this, the passwords app checks on a regular basis if one of your passwords appears in these databases and notifies you if it does.
This does not necessarily mean that you or the website which you use the password for have been hacked.
But you should change the password as hackers now have it in their databases as well.

#### Password tells me that one of my passwords could not be shared
Given that the option is enabled, you can share passwords which have been shared with you.
By doing so, it might happen that the person you want to share the password with, is the one who originally shared it.
If that is the case, Passwords will not complete the sharing process as this would create an endless loop.