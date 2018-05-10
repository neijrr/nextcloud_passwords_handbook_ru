# Available api actions
| Action | Url | Method | Description |
| --- | --- | --- | --- |
| get   | `/api/1.0/settings/get`   | POST | Returns the value of one setting |
| set   | `/api/1.0/settings/set`   | POST | Sets the value of a setting |
| list  | `/api/1.0/settings/list`  | GET  | Lists all settings |
| list  | `/api/1.0/settings/list`  | POST | Lists all settings in a scope |
| reset | `/api/1.0/settings/reset` | POST | Resets a setting |




# Scopes and Settings
| Scope | Writable | Description |
| --- | --- | --- |
| user | yes | User specific settings |
| client | yes | Client specific settings |
| server | no | Server specific settings |

| Setting | Type | Default | Description |
| --- | --- | --- | --- |
| user.password.generator.strength | int | 1 | The strength of generated passwords |
| user.password.generator.numbers | bool | false | Whether or not generated passwords contain numbers |
| user.password.generator.special | bool | false | Whether or not generated passwords contain special characters |
| user.mail.security | bool | true | Whether or not the user receives mails about security issues |
| user.mail.shares | bool | false | Whether or not the user receives mails about new shared objects |
| user.notification.security | bool | true | Whether or not the user receives notifications about security issues |
| user.notification.shares | bool | true | Whether or not the user receives notifications about new shared objects |
| user.notification.errors | bool | true | Whether or not the user receives notifications about backgroudn errors |
| server.version | string | - | The Nextcloud version of the server |
| server.baseUrl | string | - | The base url of the server |
| server.baseUrl.webdav | string | - | The base url of the WebDav service used for file storage |
| server.sharing.enabled | bool | true | Whether or not sharing is enabled globally |
| server.sharing.resharing | bool | true | Whether or not resharing shared entities is enabled globally |
| server.sharing.autocomplete | bool | true | Whether or not the [auto-complete](./Share-Api.md#the-partners-action) request works |
| server.sharing.types | array | `["user"]` | List of supported sharing types.  |
| server.theme.color | string | `#745bca` | The color of the current Nextcloud theme |
| server.theme.text.color | string | `#ffffff` | The contrast color of the current Nextcloud theme |
| server.theme.background | string | - | The url to the current Nextcloud background image |
| server.theme.logo | string | - | The url to the logo of the current Nextcloud theme |
| server.theme.label | string | "Nextcloud" | The name of the Nextcloud instance |
| server.theme.folder.icon | string | - | The url to the current svg folder icon |
| server.manual.url | string | - | The base url of the in-app user handbook |
| client.* | - | null | The client scope allows client defined keys |

#### Notes
 - The `server.theme.background` image might have a transparent background. In this case the background color should be `server.theme.color`.
 - The `client` scope allows keys with up to 48 characters, excluding `client.`
 - The `client` scope allows values with a maximum length of 128 characters
 - The `client` scope is shared between all clients




# The get action
Get the value of one or more settings.
This action accepts an array of strings where each value is the name of one setting.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| first setting | string | - | yes | The name of the first setting |
| second setting | string | - | no | The name of the second setting |

#### Return value
The success status code is `200 Ok`.
The return value is an object with the requested settings.
Each key of the object is a setting and the value is the value of the setting.

#### Notes
 - The Enhanced API also offers the option to get a single setting
 - If the setting is not defined, it will default to `null`
 - Accessing an undefined setting in the `client` scope will not create it




# The set action
Set the value of one or more settings.
This action accepts an object where each key is the name of a setting and the value is the new value

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| first setting | mixed | - | yes | The first setting to be set |
| second setting | mixed | - | no | The second setting to be set |

#### Return value
The success status code is `200 Ok`.
The return value is an object with the updated settings and their new value.

#### Notes
 - The Enhanced API also offers the option to set a single setting
 - If the scope is not writable, the setting will not be saved and default to `null` in the return value
 - If the setting is not defined in the `user` scope, it will not be saved and default to `null` in the return value
 - If the size limitations of the `client` scope are exceeded, an error will be returned




# The reset action
Reset the value of one or more settings.
This action accepts an array of strings where each value is the name of one setting.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| first setting | string | - | yes | The name of the first setting |
| second setting | string | - | no | The name of the second setting |

#### Return value
The success status code is `200 Ok`.
The return value is an object with the cleared settings.
Each key of the object is a setting and the value is the value of the setting.

#### Notes
 - If you reset a setting in the client scope, it will be deleted and no longer appear in the list action
 - If the setting does not exist, the value will be `null`




# The list action
Lists all settings within a scope.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| scopes | array | - | no | An array with the names of all requested scopes as value |

#### Return value
The return value is a JSON formatted object with all settings from the requested scopes.

#### Notes
 - If a scope has been specified, only the values of this scope will be returned
 - If the specified scopes do not exist, te return value is an empty array
 - If no scope has been defined, all existing settings will be returned




# Known client settings
| Setting | Type | Default |Allowed Values | Description |
| --- | --- | --- | --- | --- |
| client.ui.section.default | string | `all` | `all`, `favourites`, `folders`, `tags`, `recent` | Which section to show when the app ist loaded |
| client.ui.password.field.title | string | `label` | `label`, `website` | Which field to use as title of a password |
| client.ui.password.field.sorting | string | `byTitle` | `byTitle`, `label`, `website` | Sort passwords by this field instead of the label. `byTitle` means use the `title` setting |
| client.ui.password.click.action | string | `password` | `password`, `username`, `url`, `details` | Copy the choosen attribute to clipboard when the user clicks on the password oropen the `details` view. |
| client.ui.password.dblClick.action | string | `username` | `password`, `username`, `url`, `details` | Copy the choosen attribute to clipboard when the user double clicks on the password oropen the `details` view. |
| client.ui.password.menu.copy | bool | `false` | - | Show "copy to clipboard" options in the password menu |
| client.ui.password.user.show | bool | `false` | - | Show the user name in the list view |
| client.ui.custom.fields.show.hidden | bool | `false` | - | Show hidden custom fields in the ui |
| client.ui.list.tags.show | bool | `false` | - | Show tags in the list view |
| client.settings.advanced | bool | `false` | - | Show advanced settings |