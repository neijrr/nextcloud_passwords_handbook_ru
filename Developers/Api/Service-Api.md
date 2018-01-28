# Available api actions
| Action | Url | Method | Description |
| --- | --- | --- | --- |
| password | `/api/1.0/service/password` | GET | Generates a password with the users default settings |
| password | `/api/1.0/service/password` | POST | Generates a password with the given settings |
| avatar   | `/api/1.0/service/avatar/{user}/{size}` | GET | Returns the avatar image for a user |
| favicon  | `/api/1.0/service/favicon/{domain}/{size}` | GET | Returns a favicon image for a domain |
| preview  | `/api/1.0/service/preview/{domain}/{view}/{width}/{height}` | GET | Returns a preview image for a domain |