[[_TOC_]]

# The Folder Object
| Property | Type | Writable | Encrypted | Versioned | Description |
| --- | --- | --- | --- | --- | --- |
| id | string | no | no | no | The UUID of the folder |
| created | int | no | no | no | Unix timestamp when the folder was created |
| updated | int | no | no | yes | Unix timestamp when the folder was updated |
| edited | int | yes | no | yes | Unix timestamp when the user last changed the folder name |
| revision | string | no | no | yes | UUID of the current revision |
| label | string | yes | yes | yes | User defined label of the folder |
| parent | string | no | no | yes | UUID of the parent folder |
| cseType | string | yes | no | yes | Type of the used client side encryption |
| sseType | string | yes | no | yes | Type of the used server side encryption |
| hidden | bool | yes | no | yes | Hides the folder in list / find actions |
| trashed | bool | no | no | yes | True if the folder is in the trash |
| favourite | bool | yes | no | yes | True if the user has marked the folder as favourite |

#### Detail Levels
| Level | Description |
| --- | --- |
| model | Returns the base model |
| +revisions | Adds the revisions property which contains all revisions. A revision consists of all properties marked as versioned and its own created property |
| +parent | Fills the parent property with the base model of the parent folder |
| +folders | Adds the folders property with the base model of all folders in this folder |
| +passwords | Adds the passwords property with the base model of all passwords in this folder |

#### Enhanced API special properties
The properties "revisions", "parent", "folders" and "passwords" are also processed if necessary.

| Property | Type | Description |
| --- | --- | --- |
| type | string | Object type, the value is "folder" |
| icon | string | Url for the default fodler favicon |
| created | Date | Date when the folder was created |
| updated | Date | Date when the folder was last updated |
| edited | Date | Date when the user last renamed the folder |

#### Notes
 - The folder uuid can be the value `00000000-0000-0000-0000-000000000000`. This is the uuid of the base folder
 - The base folder can not be edited at all


# Available api actions
| Action | Url | Method | Description |
| --- | --- | --- | --- |
| list | `/api/1.0/folder/list` | GET | List all folders with the default detail level |
| list | `/api/1.0/folder/list` | POST | List all folders with the given detail level |
| show | `/api/1.0/folder/show` | POST | Show a folder |
| find | `/api/1.0/folder/find` | POST | Find folders matching given criteria |
| create | `/api/1.0/folder/create` | POST | Create a new folder |
| update | `/api/1.0/folder/update` | PATCH | Update an existing folder |
| delete | `/api/1.0/folder/delete` | DELETE | Delete a folder |
| restore | `/api/1.0/folder/restore` | PATCH | Restore an earlier state of a folder |


# The create action
The create action creates a new folder with the given attributes.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| label | string | - | yes | The label of the folder |
| parent | string | Base folder | no | The current parent folder |
| cseType | string | "none" | no | The client side encryption type |
| edited | int | 0 | no | Unix timestamp when the user has last renamed the folder |
| hidden | bool | false | no | Whether or not the folder should be hidden |
| favourite | bool | false | no | Whether or not the user has marked this folder as favourite |

#### Return value
The success status code is `201 Created`

| Argument | Type | Description |
| --- | --- | --- |
| id | string | The UUID of the folder |
| revision | string | The UUID of the revision |

#### Notes
 - If the uuid of the parent folder is invalid or does not exist, the base folder uuid will be used instead
 - If the folder is not hidden and should be created in a hidden folder, it will be created in the default folder instead
 - If the `edited` argument is "0", missing or in the future, the current time will be used


# The update action
The update action creates a new revision of a folder with an updated set of attributes.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| id | string | - | yes | The id of the password object |
| label | string | - | yes | The label of the folder |
| parent | string | Base folder | no | The current parent folder |
| cseType | string | "none" | no | The client side encryption type |
| edited | int | 0 | no | Unix timestamp when the user has last renamed the folder |
| hidden | bool | false | no | Whether or not the folder should be hidden |
| favourite | bool | false | no | Whether or not the user has marked this folder as favourite |


#### Return value
The success status code is `200 Ok`

| Argument | Type | Description |
| --- | --- | --- |
| id | string | The UUID of the folder |
| revision | string | The UUID of the new revision |

#### Notes
 - If the uuid of the parent folder is invalid or does not exist, the base folder uuid will be used instead
 - If the folder is not hidden and should be moved to a hidden parent folder, it will be moved to the default folder instead
 - If hou hide a folder, all folders and passwords in it will be hidden as well
 - If you unhide a folder no change to the folders and passwords in it will be made and they will remain hidden
 - If the `edited` argument is "0" or missing, the timestamp from the last revision will be used
 - If the `edited` time is in the future, the current time will be used