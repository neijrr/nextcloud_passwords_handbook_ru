# The Share Object
| Property | Type | Writable | Description |
| --- | --- | --- | --- |
| id | string | no | The UUID of the share |
| created | int | no | Unix timestamp when the share was created |
| updated | int | no | Unix timestamp when the share was updated |
| expires | int | yes | Unix timestamp when the share will expire |
| editable | bool | yes | Whether or not the receiving user can edit the password |
| shareable | bool | yes | Whether or not the receiving user can share the password again |
| updatePending | bool | no | Whether or not data changes for this share are in queue |
| password | string | yes | The UUID of the password |
| owner | object | yes | Object with the id and the full name of the owner |
| receiver | object | yes | Object with the id and the full name of the receiver |

#### Detail Levels
| Level | Description |
| --- | --- |
| model | Returns the base model |
| +password | Fills the password property with the base model of the password |

#### Enhanced API special properties
The property "password" is also processed if necessary.

| Property | Type | Description |
| --- | --- | --- |
| type | string | Object type, the value is "share" |
| created | Date | Date when the share was created |
| updated | Date | Date when the share was last updated |
| expires | Date | Date when the share will expire |
| owner.icon | string | Url of the default avatar icon of the owner in 32x32px |
| receiver.icon | string | Url of the default avatar icon of the receiver in 32x32px |

#### Notes
 - Shares have no revisions
 - The value of the `password` attribute is different for the owner and the receiver
 - The `shareable` will always be `false` for the receiver if resharing is disabled system wide


# Available api actions
| Action | Url | Method | Description |
| --- | --- | --- | --- |
| info | `/api/1.0/share/info` | GET | Returns information about the share api capabilities |
| list | `/api/1.0/share/list` | GET | List all shares with the default detail level |
| list | `/api/1.0/share/list` | POST | List all shares with the given detail level |
| show | `/api/1.0/share/show` | POST | Show a share |
| find | `/api/1.0/share/find` | POST | Find shares matching given criteria |
| create | `/api/1.0/share/create` | POST | Create a new share |
| update | `/api/1.0/share/update` | PATCH | Update an existing share |
| delete | `/api/1.0/share/delete` | DELETE | Delete a share |
| partners | `/api/1.0/share/partners` | GET | Find users you can share with |
| partners | `/api/1.0/share/partners` | POST | Find users you can share with by pattern |


# The info action
This command lists the status of the available features of the sharing api.

#### Return value
The success status code is `200 Ok`

| Argument | Type | Description |
| --- | --- | --- |
| enabled | bool | Whether or not the sharing api is enabled |
| resharing | bool | Whether or not resharing is allowed systemwide |
| autocomplete | bool | Whether or not the `partners` action is enabled |
| types | array | A list of supported sharing types |


# The partners action
This commands returns an array of users that the current user can share with.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| search | string | - | no | Find users containing the search string |

#### Return value
The success status code is `200 Ok`.
The return value is an array with the user id as key and the user display name as value.
The array is at maximum around 512 entries long.
If the autocompletion is disabled by the administrator the result is an empty array

#### Notes
 - This command will not work if sharing is disabled