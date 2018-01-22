**Contents**

[[_TOC_]]

# The Password Object
| Property | Type | Writable | Encrypted | Versioned | Description |
| --- | --- | --- | --- | --- | --- |
| id | string | no | no | no | The UUID of the password |
| created | int | no | no | no | Unix timestamp when the password was created |
| updated | int | no | no | yes | Unix timestamp when the password was updated |
| edited | int | yes | no | yes | Unix timestamp when the user last changed the password |
| share | string / null | no | no | no | UUID of the share if the password was shared by someone else with the user |
| revision | string | no | no | yes | UUID of the current revision |
| label | string | yes | yes | yes | User defined label of the password | 
| username | string | yes | yes | yes | Username associated with the password |
| password | string | yes | yes | yes | The actual password |
| notes | string | yes | yes | yes | Notes for hte password. Can be formatted with Markdown |
| url | string | yes | yes | yes | Url of the website |
| status | int | no | no | yes | Security status of the password |
| hash | string | yes | no | yes | SHA1 hash of the password |
| folder | string | yes | no | yes | UUID of the current folder of the password |
| cseType | string | yes | no | yes | Type of the used client side encryption |
| sseType | string | yes | no | yes | Type of the used server side encryption |
| hidden | bool | yes | no | yes | Hides the password in list / find actions |
| trashed | bool | no | no | yes | True if the password is in the trash |
| favourite | bool | yes | no | yes | True if the user has marked the password as favourite |
| editable | bool | no | no | no | Specifies if the encrypted properties can be changed. Might be false for shared passwords |

#### Detail Levels
| Level | Description |
| --- | --- | 
| model | Returns the base model |
| +revisions | Adds the revisions property which contains all revisions. A revision consists of all properties marked as versioned and its own created property |
| +folder | Fills the folder property with the base model of the folder |
| +tags | Adds the tags property filled with the base model of all tags |
| +shares | Adds the shares property filled with the base model of all shares with other users. Fills the share property with the base model of the original share if available |

#### Enhanced API special properties
The properties "revisions", "folder", "tags", "shares" and "share" are also processed if necessary.

| Property | Type | Description |
| --- | --- | --- | 
| type | string | Object type, the value is "password" |
| icon | string | Url for the default favicon of the website |
| image | string | Url for the default website preview image |
| created | Date | Date when the password was created |
| updated | Date | Date when the password was last updated |
| edited | Date | Date when the use last changed the password |

#### Notes
 - The status property may be 0 for secure, 1 for weak and 2 for broken.
 Since not all password analysis can be done server side, some passwords may be classified as 0 even if they fail the users password rules.
 The users password rules need to be checked client sided.


# Available api actions
| Action | Url | Method | Description |
| --- | --- | --- | --- |
| list | `/api/1.0/password/list` | GET | List all passwords with the default detail level |
| list | `/api/1.0/password/list` | POST | List all passwords with the given detail level |
| show | `/api/1.0/password/show` | POST | Show a password |
| find | `/api/1.0/password/find` | POST | Find passwords matching given criteria |
| create | `/api/1.0/password/create` | POST | Create a new password |
| update | `/api/1.0/password/update` | PATCH | Update an existing password |
| delete | `/api/1.0/password/delete` | DELETE | Delete a password |
| restore | `/api/1.0/password/restore` | PATCH | Restore an earlier state of a password |


# The create method
The create method creates a new password with the given attributes

#### Attributes
| Attribute | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| password | string | - | yes | The password |
| label | string | - | yes | The label of the password |
| username | string | empty | no | The username associated with the password |
| url | string | empty | no | The url of the associated website |
| notes | string | empty | no | The users notes |
| hash | string | empty | yes | The SHA1 hash of the password |
| cseType | string | "none" | no | The client side encryption type |
| folder | string | Base folder | no | The current folder of the password |
| hidden | bool | false | no | Whether or not the password should be hidden |
| favourite | bool | false | no | Whether or not the user has marked this password as favourite |
| tags | array | empty | no | The id of all tags associated with this passwords. Tags have to exist and can not be created inline |

#### Return value
The success status code is `201 Created`

| Attribute | Type | Description |
| --- | --- | --- |
| id | string | The UUID of the password |
| revision | string | The UUID of the revision |