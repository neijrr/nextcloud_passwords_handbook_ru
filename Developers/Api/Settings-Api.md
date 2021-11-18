The settings api allows clients to get and set settings in the user account.

# Available api actions
| Action | Url | Method | Session required | Description |
| --- | --- | --- | --- | --- |
| [get](#the-get-action)   | `/api/1.0/settings/get`   | POST | no  | Returns the value of one setting |
| [set](#the-set-action)   | `/api/1.0/settings/set`   | POST | yes | Sets the value of a setting |
| [list](#the-list-action)  | `/api/1.0/settings/list`  | GET  | no  | Lists all settings |
| [list](#the-list-action)  | `/api/1.0/settings/list`  | POST | no  | Lists all settings in a scope |
| [reset](#the-reset-action) | `/api/1.0/settings/reset` | POST | yes | Resets a setting |




# Scopes and Settings
| Scope | Writable | Description |
| --- | --- | --- |
| user | yes | Settings for the current user account. Used to configure backend/api behaviour |
| client | yes | Client settings. Accessible to all clients attached to the user account |
| server | no | Server settings, configured by the admin |

| Setting | Type | Default | Description |
| --- | --- | --- | --- |
| user.password.generator.strength | int | 1 | The strength of generated passwords, a value between 0 (weak) and 4 (strong) |
| user.password.generator.numbers | bool | false | Whether or not generated passwords contain numbers |
| user.password.generator.special | bool | false | Whether or not generated passwords contain special characters |
| user.password.security.duplicates | bool | true | Whether or not the server should check passwords for duplicates |
| user.password.security.age | int | 0 | Marks passwords a weak if they surpass the specified date mark. 0 is off. |
| user.password.security.hash | int | 40 | How many characters of the has should be saved. Can be either 0, 20, 30 or 40. For e2e this is implemented by the client, count characters from the beginning of the string |
| user.mail.security | bool | true | Whether or not the user receives mails about security issues |
| user.mail.shares | bool | false | Whether or not the user receives mails about new shared objects |
| user.notification.security | bool | true | Whether or not the user receives notifications about security issues |
| user.notification.shares | bool | true | Whether or not the user receives notifications about new shared objects |
| user.notification.errors | bool | true | Whether or not the user receives notifications about background errors |
| user.notification.admin | bool | true | Whether or not the user receives notifications about configuration issues. Only for admins |
| user.encryption.sse | int | 1 | The server side encryption type. 0 = None, 1 = SSEv1, 2 = SSEv1 |
| user.encryption.cse | int | 0 | The client side encryption type. 0 = None, 1 = CSEv1 |
| user.sharing.editable | bool | true | Whether or not the editable option should be set by default for a new share. Not writeable if sharing disabled. |
| user.sharing.resharing | bool | true | Whether or not the resharing option should be set by default for a new share. Not writeable if sharing or resharing disabled. |
| user.session.lifetime | int | 600 | The session lifetime in seconds |
| server.version | string | - | The Nextcloud version of the server, e.g. "20" |
| server.app.version | string | - | The app version of the server, e.g. "2020.9" |
| server.baseUrl | string | - | The base url of the server |
| server.baseUrl.webdav | string | - | The base url of the WebDav service used for file storage |
| server.sharing.enabled | bool | true | Whether or not sharing is enabled globally |
| server.sharing.resharing | bool | true | Whether or not resharing shared entities is enabled globally |
| server.sharing.autocomplete | bool | true | Whether or not the [auto-complete](./Share-Api.md#the-partners-action) request works |
| server.sharing.types | array | `["user"]` | List of supported sharing types.  |
| server.theme.color.primary | string | `#745bca` | The color of the current Nextcloud theme |
| server.theme.color.text | string | `#ffffff` | The text color of the current Nextcloud theme |
| server.theme.color.background | string | `#ffffff` | The background color of the current Nextcloud theme |
| server.theme.background | string | - | The url to the current Nextcloud background image |
| server.theme.logo | string | - | The url to the logo of the current Nextcloud theme |
| server.theme.label | string | "Nextcloud" | The name of the Nextcloud instance |
| server.theme.app.icon | string | - | The url to the current svg app icon |
| server.theme.folder.icon | string | - | The url to the current svg folder icon |
| server.handbook.url | string | - | The base url of the in-app user handbook |
| server.performance | int | 2 | An integer value indicating the server performance preference. 0 is a slow server where requests should be avoided (max 1 simultaneous request), 5 is a fast server which can handle many requests (x * 3 simultaneous requests), 6 is for unlimited requests. |
| client.* | - | null | The client scope allows client defined keys |

#### Notes
 - The `server.theme.background` image might have a transparent background. In this case the background color should be `server.theme.color`.
 - The `client` scope allows keys with up to 48 characters, excluding `client.`
 - The `client` scope allows values with a maximum length of 128 characters
 - The `client` scope is shared between all clients




# The get action
The get action retrieves the value of one or more settings.
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
The set action updates the value of one or more settings.
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
The reset actionwill reset the value of one or more settings to the default.
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
The list action returns all settings or the settings within a scope if one is given.

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
| client.ui.section.default | string | `all` | `all`, `favorites`, `folders`, `tags`, `recent` | Which section to show when the app ist loaded |
| client.ui.password.field.title | string | `label` | `label`, `website` | Which field to use as title of a password |
| client.ui.password.field.sorting | string | `byTitle` | `byTitle`, `label`, `website` | Sort passwords by this field instead of the label. `byTitle` means use the `title` setting |
| client.ui.password.click.action | string | `password` | `password`, `username`, `url`, `details` | Copy the choosen attribute to clipboard when the user clicks on the password oropen the `details` view. |
| client.ui.password.dblClick.action | string | `username` | `password`, `username`, `url`, `details` | Copy the choosen attribute to clipboard when the user double clicks on the password oropen the `details` view. |
| client.ui.password.menu.copy | bool | `false` | - | Show "copy to clipboard" options in the password menu |
| client.ui.password.user.show | bool | `false` | - | Show the user name in the list view |
| client.ui.custom.fields.show.hidden | bool | `false` | - | Show custom fields with the type `data` in the ui |
| client.ui.list.tags.show | bool | `false` | - | Show tags in the list view |
| client.search.show | bool | `false` | - | Show search section in navigation |
| client.search.live | bool | `true` | - | Start search when user types |
| client.search.global | bool | `true` | - | Start global search when user hits enter |
| client.settings.advanced | bool | `false` | - | Show advanced settings |