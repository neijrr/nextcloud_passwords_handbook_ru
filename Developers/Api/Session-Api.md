# Available api actions
| Action | Url | Method | Description |
| --- | --- | --- | --- |
| request   | `/api/1.0/session/request`   | GET  | Request the information to open a session |
| open      | `/api/1.0/session/open`      | POST | Open a new session |
| close     | `/api/1.0/session/close`     | GET  | Close an existing session |
| keepalive | `/api/1.0/session/keepalive` | GET  | Keep the session alive |


# The request action
The request action must be used to request the information a client needs to provide to the `open` action in order to open a new authenticated session.

#### Arguments
| Argument | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
