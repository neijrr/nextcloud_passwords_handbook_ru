# The Share Object
| Property | Type | Writable | Description |
| --- | --- | --- | --- |
| id | string | no | The UUID of the share |
| created | int | no | Unix timestamp when the share was created |
| updated | int | no | Unix timestamp when the share was updated |
| expires | int / null | yes | Unix timestamp when the share will expire |
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
| list | `/api/1.0/share/list` | GET | List all shares with the default detail level |
| list | `/api/1.0/share/list` | POST | List all shares with the given detail level |
| show | `/api/1.0/share/show` | POST | Show a share |
| find | `/api/1.0/share/find` | POST | Find shares matching given criteria |
| create | `/api/1.0/share/create` | POST | Create a new share |
| update | `/api/1.0/share/update` | PATCH | Update an existing share |
| delete | `/api/1.0/share/delete` | DELETE | Delete a share |
| partners | `/api/1.0/share/partners` | GET | Find users you can share with |
| partners | `/api/1.0/share/partners` | POST | Find users you can share with by pattern |




# The partners action
This commands returns an array of users that the current user can share with.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| search | string | - | no | Find users containing the search string |
| limit | int | 5 | no | The maximum amount of matches to return |

#### Return value
The success status code is `200 Ok`.
The return value is an array with the user id as key and the user display name as value.
The array is at maximum around 256 entries long.
If the autocompletion is disabled by the administrator the result is an empty array

#### Notes
 - This command will fail if sharing is disabled
 - This api endpoint has a rate limit of 48 requests in 5 minutes




# The create action
The create action creates a new share with the given attributes.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| password | string | - | yes | The UUID of the password |
| receiver | string | - | yes | The user id of the user which the password should be shared with |
| type | string | "user" | no | The type of the share |
| expires | int / null | null | no | Unix timestamp when the share will expire |
| editable | bool | false | no | Whether or not the receiver can edit the password |
| shareable | bool | false | no | Whether or not the receiver can share the password |

#### Return value
The success status code is `201 Created`

| Argument | Type | Description |
| --- | --- | --- |
| id | string | The UUID of the share |

#### Notes
 - This action will fail if the password is hidden or the CSE does not support sharing
 - You can not share a password with the same user more than once
 - This command will fail if sharing is disabled




# The update action
The update action changes the properties of an existing share.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| id | string | - | yes | The UUID of the share |
| expires | int / null | null | no | Unix timestamp when the share will expire |
| editable | bool | false | no | Whether or not the receiver can edit the password |
| shareable | bool | false | no | Whether or not the receiver can share the password |

#### Return value
The success status code is `200 Ok`

| Argument | Type | Description |
| --- | --- | --- |
| id | string | The UUID of the share |

#### Notes
 - You can only edit a share if it is owned by the user
 - This command will fail if sharing is disabled




# The delete action
The delete action deletes a share.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| id | string | - | yes | The id of the share |

#### Return value
The success status code is `200 Ok`

| Argument | Type | Description |
| --- | --- | --- |
| id | string | The UUID of the share |

#### Notes
 - You can only delete shares owned by the user.
 - If you want to delete a share where the current user is the receiver, you need to delete the password instead
 - This action still works if sharing has been disabled




# The show action
The show action lists the properties of a single share.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| id | string | - | yes | The id of the share |
| detailLevel | string | "model" | no | The detail level of the returned share object |

#### Return value
The success status code is `200 Ok`
The return value is a share object with the given detail level

#### Notes
 - This action still works if sharing has been disabled




# The list action
The list action lists all shares with the user as owner or receiver.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| detailLevel | string | "model" | no | The detail level of the returned share objects |

#### Return value
The success status code is `200 Ok`
The return value is a list of share objects with the given detail level

#### Notes
 - This action still works if sharing has been disabled


# The find action
The find action can be used to find all shares matching the given search criteria.
Only a specific set of fields is allowed in the criteria.
How the criteria array works is explained on the [object search page](./Object-Search.md).

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| criteria | array | [] | no | The search criteria |
| detailLevel | string | "model" | no | The detail level of the returned share objects |

#### Allowed search fields
| Field | Type | Description |
| --- | --- | --- |
| created | int | Unix timestamp when the share was created |
| updated | int | Unix timestamp when the share was updated |
| owner | string | User id of the owner of the share |
| receiver | string | User id of the receiver of the share |
| expires | int / null | Unix timestamp when the share will expire |
| editable | bool | Whether or not the receiver can edit the password |
| shareable | bool | Whether or not the receiver can share the password |

#### Return value
The success status code is `200 Ok`
The return value is a list of shares objects that match the criteria with the given detail level

#### Notes
 - The `owner` and `receiver` fields allow the special value `_self` which is replaced with the users id
 - This action still works if sharing has been disabled