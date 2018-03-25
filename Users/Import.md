The import can be found `More > Backup and Restore > Restore or Import`.
It can be used to restore a previously made backup, import a backup from another instance or import data from another password manager.

[![The Import section](_files/import-overview.png)](_files/import-overview.png)

## The Import Steps
##### 1. Choose Format
Choose the format of the file you want to import.
If you want to import a CSV file from an application which is not listed, choose `Custom CSV`.

##### 2. Select File
Select the file you want to import.
If you want to import a custom csv file, make sure to set the csv options before you open the file.

##### 3. Select Options
Select the options for the import.
Depending on the file type, different options may be available which are explained below.

##### 4. Run Import
If you're ready to go, hit the `Import` button and start importing your files


## Import Options
##### Import Mode
The `Import Mode` defines how the Importer should handle conflicts.
`Skip if same revision` will skip entries when an object with the same id and same revision already exists in the database.
`Skip if id exists` will skip entries when the id already exists.
`Overwrite if id exists` will overwrite an entry with the data from the import if the id is found in the database.
`Clone if id exists` will create a new entry if an entry with the same id already exists.