# Available api actions
| Action | Url | Method | Description |
| --- | --- | --- | --- |
| reset         | `/api/1.0/account/reset`         | POST | Reset the user account |
| challenge/get | `/api/1.0/account/challenge/get` | GET  | Get the current login challenge |
| challenge/set | `/api/1.0/account/challenge/set` | POST | Set or update the login challenge |


# The reset action
The reset action will delete all user data and settings and reset the account to a blank state.
This is a destructive action and can only be undone with a backup.
The first request to the api endpoint will return a random wait time after which the action can be performed.
The user should have to confirm both requests individually.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| password | string | - | yes | The login password of the user |

#### Return value
The success status code is `200 Ok` or `202 Accepted`.

| Argument | Type | Description |
| --- | --- | --- |
| status | string | Either "accepted" or "ok". Ok means the action was completed |
| wait | int | Random number of seconds to wait before sending the second request |

#### Notes
 - This request will close the session
 - This request will not delete any app or device tokens


# The get challenge action
The get challenge action will return the current password challenge.
The format matches the one in of the `challenge` property from [request-session](./Session-Api#the-request-action)

#### Arguments
There are no arguments for this action.

#### Return value
The success status code is `200 Ok` .
The request returns an object with the challenge data and the property `token` which identifies the challenge type.


# The set challenge action
This action will create or update the user challenge and enable CSE and SSEv2.
It is not possible to specify the challenge type and the server always expects you to use the latest challenge method.
This is currently `PWDv1r1`.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| secret | string | - | yes | The computed secret of the new challenge |
| data | array | - | yes | An array with the challenge data |
| oldSecret | string/null | null | no | If the user already has CSE set up, the secret of the current challenge is required |

#### Return value
The success status code is `200 Ok` .
The request returns an object property success and the value true if successful.

#### Notes
 - This action will fail if the `client-side-encryption` feature is disabled on the server
 - This action will authorize the current session if successful