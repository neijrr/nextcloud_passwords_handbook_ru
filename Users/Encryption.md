> :warning: Some third-party clients do not support encryption

> :warning: You need the [development version](https://github.com/marius-wieschollek/passwords-webextension#downloads) of the browser extension to use encryption

> :star: Encryption needs to be enabled by the administrator

## Enabling Encryption
#### Important Information
By default, the encryption setup will encrypt all existing database except shared ones.
All password revisions but the current will be deleted.
The encryption setup will also create a new password entry with your master password.
If you do not want this, switch the settings view to `Advanced` in the top right corner and uncheck the options in step 5 of the setup.

#### Manual encryption setup
1. Open the Settings (`More > Settings`)
2. Locate the `Encryption` section at the end of the `Security` section.
   > :warning: If you can't see it, encryption is not enabled
3. Click the `Activate` button of `End-to-End Encryption`.
4. The setup wizard will appear. Click continue to see the master password dialog.
5. Enter the master password with at least 12 characters and confirm it.
6. Click `Save`.

The encryption setup will automatically encrypt all folders and passwords

> :exclamation: Do not abort the encryption process or reload the page