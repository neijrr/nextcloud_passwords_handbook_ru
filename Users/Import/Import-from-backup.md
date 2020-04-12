This guide explains the import from a Passwords database backup which can be created with the export.

> :star: The Passwords database backup can also be used to move from one Nextcloud instance to another

## Export from Passwords
1. Open the Passwords app.
2. Click on "More" in the bottom left corner.
3. Click on "Backup and Restore".
4. Choose "Backup or export".
5. Choose export options as wanted.
6. Click the "Export" button.
7. Wait for the export to finish, then click the "Download JSON" button.
8. Save the file on your computer

## Import into Passwords
1. Open the Passwords app.
2. Click on "More" in the bottom left corner.
3. Click on "Backup and Restore".
4. Choose "Restore or import".
5. Select "Database Backup" as import format.
6. Open the file you exported before using the file dialog.
7. Choose import options as wanted.
8. Click the "Import" button.
9. After the import has finished, check the imported passwords.
10. Delete the export file from your computer.


## Import Options

> :star: This section describes only describes the import options which are specific to the database import.
> For all other options please see [the general import options](../Import#Import-Options).

### Database Backup
Database backups are a special import source.

##### Backup password
If the backup has been secured with a password, you will have to enter it here.


## Troubleshooting
See [import troubleshotting](../Import#Troubleshooting).