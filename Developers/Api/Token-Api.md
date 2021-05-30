The token api allows clients to trigger 2FA token providers in order to send the user a 2FA token.

# Available api actions
| Action | Url | Method | Session required | Description |
| --- | --- | --- | --- | --- |
| [request](#the-request-action) | `/api/1.0/token/{provider}/request` | GET | no | Requests a token with the provider |


# The request action
The request action is required for some token in order to send the user the token.
For example the email token will send an email to the users mail account.
It is recommended to only call this action if the user has chosen that token, not just trigger it for all available tokens.

#### Arguments
| Argument | Type | Description |
| --- | --- | --- |
| provider | string | The id of the token |

#### Return value
The success status code is `200 Ok`.

| Argument | Type | Description |
| --- | --- | --- |
| success | boolean | Whether or not the action was successful |
| data | object | For the "Nextcloud Notification" token, this object will contain the property `token` with the token value. |


# Token types

### The token object
The [session request](./Session-Api#the-request-action) action will return an array of possible tokens.
Each token object looks like this:

```json
{
    "type":"user-token",
    "id":"tokenid",
    "label":"Human readable label",
    "description":"A short description of the token process",
    "request":true
}
```

| Argument | Type | Description |
| --- | --- | --- |
| type | string | The token type is either `user-token` or `request-token` |
| id | object | This id must be used in the [token request](#the-request-action) and the [session open](./Session-Api#the-open-action) action. |
| label | string | The label of the token |
| description | string | A description of the token adn the authentication process |
| request | boolean | Whether or not the authentication process must be triggered with the [request action](#the-request-action) |


### The user token
Tokens with the type `user-token` require that the user enters a code which is then sent to the server.
It might be required that the [request action](#the-request-action) is executed in order to provide the user with that code.

### The request token
Currently only the "Nextcloud Notification" is a `request-token`.
This token does not require a user input.
Instead the user will confirm the token trough a second app or device.
The [request action](#the-request-action) will provide the token that needs to be sent to the server.