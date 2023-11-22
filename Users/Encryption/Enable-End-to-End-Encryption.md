The passwords app offers strong end-to-end encryption which requires anyone trying to decrypt your passwords to know the encryption passphrase.

## Enabling End-to-End encryption

#### Important Information
- By default, the encryption setup will encrypt all existing passwords, folders and tags except those who are shared.
- All previous revisions but the current will be deleted.
- The encryption setup will also create a new password entry with your encryption passphrase.
  If you do not want this, switch the settings view to `Advanced` in the top right corner and uncheck the options in step 5 of the setup.
- The encryption setup will create the new entries before deleting any old ones.
  So even if something goes wrong, there should be no data loss.

#### Enabling End-to-End encryption
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


## Disabling End-to-End encryption
There is no built-in option to disable end-to-end encryption.
Passwords a functionality to store hidden passwords, tags and folders and also keeps previous revisions of any change made to any item.
These features prevent removing the encryption passphrase or would leave some items permanently encrypted and unreadable.
You can follow these steps to export all your data, reset the app and start again without encryption:

> :exclamation: This process will delete any hidden items and all settings

1. Make sure you have no hidden items or use the [Recover hidden items](../Settings#recover-hidden-items) option to show them all.
2. Exit or log out of any client but the Nextcloud app itself
3. Ask your admin to make a backup using passwords backup command
4. Make a complete, unencrypted [database export](./Export#database-backup)
5. Check the contents of the export with a text editor to verify that your data is exported correctly
6. Go into `Settings` and use the option to reset everything in the `Danger Zone`
7. [Import the database backup](../Import/Import-from-Backup)
8. Delete the backup file and restore your settings