The passwords app offers strong client side encryption which requires anyone trying to decrypt your passwords to know the encryption passphrase.

## Enabling Client Side Encryption
> :warning: Some third-party clients do not support encryption

#### Important Information
- By default, the encryption setup will encrypt all existing passwords, folders and tags except those who are shared.
- All previous revisions but the current will be deleted.
- The encryption setup will also create a new password entry with your encryption passphrase.
  If you do not want this, switch the settings view to `Advanced` in the top right corner and uncheck the options in step 5 of the setup.
- The encryption setup will create the new entries before deleting any old ones.
  So even if something goes wrong, there should be no data loss.

#### Enabling Client Side Encryption
1. Open the Settings (`More > Settings`)
2. Locate the `Encryption` section at the end of the `Security` section.
3. Click the `Activate` button next to `End-to-End Encryption`.
4. The setup wizard will appear. Click continue to see the encryption passphrase dialog.
5. Choose an encryption passphrase with at least 12 characters and confirm it.
   > :warning: Do not use your Nextcloud password.
   > Every Nextcloud app can read your Nextcloud password and it offers no security
6. Click `Save`.

The encryption setup will automatically encrypt all folders and passwords

> :warning: Do not abort the encryption process or reload the page


## Disabling Client Side Encryption
There is no built-in option to disable client side encryption.
Passwords offers hidden passwords, which make it impossible to guarantee that all passwords have been decrypted.
This would either prevent removing the encryption passphrase or leave some passwords unreadable and permanently encrypted.
If you're sure that you do not have any hidden passwords, you can try the following steps:

> :exclamation: This process will delete any hidden items and all settings

1. Make you have no hidden passwords in any app you use or unhide them in that app.
2. Exit or log out of any client but the Nextcloud app itself
3. Ask your admin to make a backup using passwords backup command
4. Make a complete, unencrypted [database export](./Export#database-backup)
5. Check the contents of the export with a text editor to verify that your data is exported correctly
6. Go into `Settings` and use the option to reset everything in the `Danger Zone`
7. [Import the database backup](./Import/Import-from-backup)
8. Delete the backup file and restore your settings