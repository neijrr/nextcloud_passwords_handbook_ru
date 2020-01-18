# Available api actions
| Action | Url | Method | Session required | Description |
| --- | --- | --- | --- | --- |
| request | `/api/1.0/token/{provider}/request` | GET | no | Requests a token with the provider |


# The request action
The keepalive action will prevent the session from being closed.

#### Arguments
There are no arguments for this action.

#### Return value
The success status code is `200 Ok`.
The action will return an object with the property `success` with the value `true`.