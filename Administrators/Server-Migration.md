This guide explains how to migrate the passwords database to a new server.
We recommend to do this first, because the passwords app backup will overwrite your server secret.

## With CLI/SSH Access
1. Log onto your old server and open the Nextcloud directory.
2. Get the Nextcloud secret
    ```
    ./occ config:system:get secret
    ```
3. Create a new backup
    ```
    ./occ passwords:backup:create migration
    ```
4. Get the data directory and the instance id:
    ```
    DATA_DIR="$(./occ config:system:get datadirectory)";
    INSTANCE_ID="$(./occ config:system:get instanceid)";
    ```
5. Copy the file from the old server to the new server
    ```
    scp ${DATA_DIR}/appdata_${INSTANCE_ID}/passwords/backups/migration.json.gz user@newserver.org:/path/to/new/nextcloud/
    ```
    If the file `migration.json.gz` does not exist, your server probably does not support compression and you can try the following:
    ```
    scp ${DATA_DIR}/appdata_${INSTANCE_ID}/passwords/backups/migration.json user@newserver.org:/path/to/new/nextcloud/
    ```
6. Now log onto your new server and open the Nextcloud directory
7. Get the data directory and the instance id:
    ```
    DATA_DIR="$(./occ config:system:get datadirectory)";
    INSTANCE_ID="$(./occ config:system:get instanceid)";
    ```
8. Move the backup file to the backup directory
    ```
    mv migration.json.gz ${DATA_DIR}/appdata_${INSTANCE_ID}/passwords/backups/migration.json.gz
    ```
9.  Let Nextcloud scan for new app files
    ```
    ./occ files:scan-app-data
    ```
10. Check that the app now recognizes your backup file and lists it
    ```
    ./occ passwords:backup:list
    ```
11. Restore the server secret from step 2.
    ```
    ./occ config:system:set secret --value=<server secret> --type=string
    ```
12. Restore the backup file with
    ```
    ./occ passwords:backup:restore migration
    ```
    
## With HTTPS/FTP Access
1. Install [OCC Web](https://apps.nextcloud.com/apps/occweb) on both your Nextclouds
2. Open OCC Web in your old Nextcloud
3. Get the server secret
    ```
    config:system:get secret
    ```
4. Create a new backup
    ```
    passwords:backup:create migration
    ```
5. Open your old server with FTP, open the data folder, then the `appdata_somecharcters` subfolder, then `passwords` `backups`.
6. Download the `migration.json.gz` file
7. Open your new server with FTP, open the data folder, then the `appdata_somecharcters` subfolder, then `passwords` `backups`.
    1. If the appdata folder does not exist, open OCC Web, run `config:system:get instanceid` and then create the folder with `appdata_theinstanceid`.
8. Upload the `migration.json.gz` file
9. Open OCC Web and scan for new app files
    ```
    files:scan-app-data
    ```
10. Check that the app now recognizes your backup file and lists it with OCC Web
    ```
    passwords:backup:list
    ```
11. Restore the server secret from step 2 with OCC Web
    ```
    config:system:set secret --value=<server secret> --type=string
    ```
12. Restore the backup file in OCC Web with
    ```
    passwords:backup:restore migration
    ```