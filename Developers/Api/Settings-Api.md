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
| theme | no | Nextcloud theme settings |

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
| client.* | - | null | The client scope allows client defined keys |

#### Notes
 - The `server.theme.background` image might have a transparent background. In this case the background color should be `server.theme.color`.
 - The `client` scope allows keys with up to 16 characters, excluding `client.`
 - The `client` scope allows values with a maximum length of 36 characters




# The get action
Get the value of one or more settings.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| <setting name> | string | - | yes | The name of the setting |

#### Return value
The success status code is `200 Ok`. The return value is an array with the requested settings

#### Notes
 - The Enhanced API also offers the option to get a single setting




# The set action
Set the value of one or more settings.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| <settings> | array | - | yes | An array with the settings |

#### Return value
The success status code is `200 Ok`. The return value is an array with the changed settings




# The reset action
Resets the value of a setting. If the setting is in the `client` scope, it will be deleted

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| key | string | - | yes | The name of the setting |

#### Return value
| Argument | Type | Description |
| --- | --- | --- |
| status | string | Is set to `ok` if the action was successful |
| key | string | The name of the setting |
| value | int | The new value of the setting |

#### Notes
 - If you reset a setting in the client scope, it will be deleted




# The list action
Resets the value of a setting. If the setting is in the `client` scope, it will be deleted

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| scope | string | - | no | The name of the scope |

#### Return value
The return value is a JSON formatted object with all scopes and their settings.
```json
{
    "server": {
        "baseUrl": "https://localhost"
    },
    "theme" : {
        "color"      : "#6AC97D",
        "text.color" : "#000000",
        "background" : "https://example.com/core/img/background.png",
        "logo"       : "https://example.com/core/img/logo.svg?v=3",
        "label"      : "Nextcloud",
        "folder.icon": "https://example.com/index.php/apps/theming/img/core/filetypes/folder.svg"
    },
    "user"  : {
        "password.generator.strength": 1,
        "password.generator.numbers": true,
        "password.generator.special": false
    },
    "client": [ ]
}
```

#### Notes
 - If a scope has been specified, only the values of this scope will be returned