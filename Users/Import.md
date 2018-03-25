The import can be found `More > Backup and Restore > Restore or Import`.
It can be used to restore a previously made backup, import a backup from another instance or import data from another password manager.

![The Import section](_files/import-overview.png)

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
**Note:** For all formats except `Database Backup`, the import will match the passwords by their name.

##### Don't edit passwords shared with me
If this option is selected, passwords which were shared with you by other users will not be overwritten by the import.


## Import specific options and notes
### Database Backup
##### Backup password
If the backup has been secured with a password, you will have to enter it here.


## How to fix faulty CSV files
![Warning for bad exports](_files/import-faulty-csv.png)
Some password managers create faulty export files which can not be parsed by the importer.
These files need to be fixed manually in order to work properly.

1. Open the file in a spreadsheet program like [LibreOffice Calc](https://libreoffice.org) or Microsoft Excel.
2. Check the file for errors. Most of these programs do a good job in fixing faulty CSVs. You should make sure that all colums are filled in properly.
3. Export the file as CSV.
4. Try the Import again

##### Example errors
![Quotes are not escaped properly](_files/import-faulty-csv-error.png)

