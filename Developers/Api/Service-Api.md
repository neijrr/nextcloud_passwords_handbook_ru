# Available api actions
| Action | Url | Method | Description |
| --- | --- | --- | --- |
| password | `/api/1.0/service/password` | GET | Generates a password with the users default settings |
| password | `/api/1.0/service/password` | POST | Generates a password with the given settings |
| avatar   | `/api/1.0/service/avatar/{user}/{size}` | GET | Returns the avatar image for a user |
| favicon  | `/api/1.0/service/favicon/{domain}/{size}` | GET | Returns a favicon image for a domain |
| preview  | `/api/1.0/service/preview/{domain}/{view}/{width}/{height}` | GET | Returns a preview image for a domain |




# The password action
The password action generates one password with the given settings.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| strength | int | 1 | no | How many words the password should have |
| numbers | bool | false | no | Whether or not numbers should be used in the password |
| special | bool | false | no | Whether or not special characters should be used in the password |
| smileys | bool | false | no | Whether or not strings like text smileys should be used in the password |

#### Return value
The success status code is `200 Ok`

| Argument | Type | Description |
| --- | --- | --- |
| password | string | The generated password |
| words | string | The words used in the password |
| strength | int | The words used in the password |
| numbers | bool | Whether or not numbers were used in the password |
| special | bool | Whether or not special characters were used in the password |
| special | bool | Whether or not smileys were used in the password |

#### Notes
 - If you call this action with a GET request, the users settings will be used
 - If you call this action with a POST request, the default settings will be used for missing parameters




# The avatar action
The avatar action returns a png avatar icon for the given user id.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| user | string | - | yes | The user id |
| size | int | 32 | no | The size of the avatar in pixels |

#### Return value
The success status code is `200 Ok`.
This action returns a png image file on success

#### Notes
 - If the user did not specify an avatar a default image will be generated
 - The size must be a multiple of `8`
 - The minimum size is `16` pixels
 - The maximum size is `256` pixels




# The favicon action
The favicon action returns a png favicon icon for the given domain.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| domain | string | - | yes | The domain name |
| size | int | 32 | no | The size of the favicon in pixels |

#### Return value
The success status code is `200 Ok`.
This action returns a png image file on success

#### Notes
 - If no favicon can be found a default image will be generated
 - The size must be a multiple of `8`
 - The minimum size is `16` pixels
 - The maximum size is `256` pixels




# The preview action
The preview action returns a jpeg preview image for the given domain.

#### Arguments
| Arguments | Type | Default | Required | Description |
| --- | --- | --- | --- | --- |
| domain | string | - | yes | The domain name |
| view | string | "desktop" | no | Can be `desktop` or `mobile`. Sets device name / viewports. |
| width | string/int | 640 | no | The width of the resulting image |
| height | string/int | "360..." | no | The height of the resulting image |

#### Return value
The success status code is `200 Ok`.
This action returns a jpeg image file on success

#### Notes
 - If no image can be created a default image will be used
 - This action is known to be slow if the cache is empty
 - The width and height must be a multiple of `10`
 - The minimum width is `240` pixels
 - The maximum width is `1280` pixels
 - The minimum height is `240` pixels
 - The maximum height is `1280` pixels
 - If a width and height were specified, the image will be cropped to fill the area
 - The width and height can be `0`. In this case, it is up to the api to set the optimal value
 - You can specify a range for width and height by passing `SIZE...`, `SIZE...SIZE` or `...SIZE` where size is a number.
   The left value will be the minimum and the right value the maximum.
   The api will try to generate an image that fits the given values without cropping
 - The resulting image will always have a minimum width and height of 240 pixels