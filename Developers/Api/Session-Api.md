# Available api actions
| Action | Url | Method | Session required | Description |
| --- | --- | --- | --- | --- |
| request   | `/api/1.0/session/request`   | GET  | no | Request the information to open a session |
| open      | `/api/1.0/session/open`      | POST | no | Open a new session |
| close     | `/api/1.0/session/close`     | GET  | no | Close an existing session |
| keepalive | `/api/1.0/session/keepalive` | GET  | no | Keep the session alive |


# The request action
the request action returns all requirements that the client must meet in order to open an authenticated session.

#### Arguments
There are no arguments for this action.

#### Return value
The success status code is `200 Ok`.
The returned object only contains a challenge or token if the user has set those up.
If nothing is required, the result is an empty object.

| Argument | Type | Description |
| --- | --- | --- |
| challenge | object | An object with the [password challenge](./Encryption#password-challenge). The property `type` specifies the challenge type. |
| token | array | An array with available [2FA token](./Token-Api). One of them must be used. |


# The open action
The open action will open an authenticated session with read and write access to all api endpoints.

#### Arguments
Which arguments are required can be found out with the request action.

| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| challenge | string | - | yes (if enabled) | The solution of the [password challenge](./Encryption#password-challenge) |
| token | object | - | yes (if enabled) | An object with the id of the token as property and the token as value |

#### Return value
The success status code is `200 Ok`.
The `keys` property is only available if encryption is used.

| Argument | Type | Description |
| --- | --- | --- |
| success | boolean | Whether or not the action was successful |
| keys | object | An object with the CSE keychains. The name of the property is the keychain and the value are the encrypted keychain contents |

#### Notes
 - This api endpoint has a rate limit of 6 requests per minute
 - After five failed login attempts, the client will be [deauthorized](#client-deauthorization).
 - If the `token` argument is provided with more than one token, all of them have to be correct or the validation will fail


# The close action
The close action will close the current session.

#### Arguments
There are no arguments for this action.

#### Return value
The success status code is `200 Ok`.
The action will return an object with the property `success` with the value `true`.


# The keepalive action
The keepalive action will prevent the session from being closed.

#### Arguments
There are no arguments for this action.

#### Return value
The success status code is `200 Ok`.
The action will return an object with the property `success` with the value `true`.

#### Notes
 - The setting `user.session.lifetime` determines the session lifetime


# Session ID
Usually, the session cookies provided by Nextcloud are sufficient to use sessions.
If for some reason your client is unable to use cookies, the special header `X-API-SESSION` can be used to exchange session ids.
The api will include the header in each request response and will accept it in each request.


# Backwards compatibility
To remain compatible with older clients which do neither support encryption nor sessions, the api does currently not require an authorized session if the user does not use encryption.

This will change by the end of 2020.


# Client deauthorization
If a client tries to open an authorized session with invalid credentials more than five times, it will be blocked.

If the client used an app or device token to access the api, the token will be deleted.
If the client used the password to access the api, the api will no longer accept password authentication.

The user will receive a notification about the incident.