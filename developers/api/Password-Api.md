# Passwords API

### The Password Object

```json
{
    "id"       : "00000000-0000-0000-0000-000000000000",
	"owner"    : "string",
	"created"  : 1513946292,
	"updated"  : 1513946292,
	"revision" : "00000000-0000-0000-0000-000000000000",
	"label"    : "string",
	"username" : "string",
	"password" : "string",
	"notes"    : "string",
	"url"      : "string",
	"status"   : 0,
	"hash"     : "string",
	"folder"   : "00000000-0000-0000-0000-000000000000",
	"cseType"  : "string",
	"sseType"  : "string",
	"hidden"   : false,
	"trashed"  : false,
	"favourite": false
}
```

| Field | Detail Level | Type | Writeable | Description |
| --- | --- | --- | --- | --- |
| id | model | string | no | The UUID of the password |
| owner | model | string | no | The Nextcloud username of the owner |
| created | model | int / Date | no | The time when the password was created. Usually a Unix timestamp, but a date object in the extended API. |
| updated | model | int / Date | no | The time when the password was last updated. Usually a Unix timestamp, but a date object in the extended API. |
| revision | model | string | no | The UUID of the current password revision |
| label | model | string | yes | The label of the password |
| username | model | string | yes | The username of the account |
| notes | model | string | yes | The notes for the password. Notes contain mardown styled text. |
| url | model | string | yes | The url of the website |
| status | model | int | no | The security status of the password |
| hash | model | string | yes | SHA-1 hash of the password. This is used to check if the password is in the HIBP database. |
| folder | model | string | yes | The UUID of the folder which the password is currently assigned to. |
| cseType | model | string | yes | The client side encryption method used to encrypt the data |
| sseType | model | string | yes | The server side encryption method used to encrypt the data |
| hidden | model | boolean | yes | Hides the password in show and find request and relations. |
| trashed | model | boolean | no | True if the password is in the trash |
| favourite | model | boolean | yes | True if the password is mared as favourite |

### Create a Password