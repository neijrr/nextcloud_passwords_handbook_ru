The hashes API returns the SHA-1 hashes of passwords contained in public data breaches.
The data can be searched by providing a SHA-1 hash or at least the first five characters of the hash.

# Contents
[[_TOC_]]

# Privacy
The Passwords app usually saves the full SHA-1 has of a password alongside the password to enable automatic checks for breached passwords.
Users can choose to disable this check or just store a partial hash to improve their privacy.
Therefore, this API supports a [k-anonymity](https://en.wikipedia.org/wiki/K-anonymity) approach in which the client requests all hashes within a given range and then confirms locally if a hash is within the set returned by the server.

# Version History
| App Version | Change                                                   |
|-------------|----------------------------------------------------------|
| 2024.1.0    | Initial introduction of the API                          |
| 2024.2.0    | API now uses 404 status code. Addition of request limits |

# Endpoints

## GET hashes endpoint
Get hashes by the given range.

#### URL
| Path                              | Method | Session required |
|-----------------------------------|--------|------------------|
| `/api/1.0/service/hashes/{range}` | GET    | no               |

#### Arguments
| Arguments | Type   | Default | Required | Description                                                      |
|-----------|--------|---------|----------|------------------------------------------------------------------|
| range     | string | -       | yes      | 5-40 characters of a SHA-1 hash to check against in the database |

#### Restrictions
- Authentication required
- User rate limit: 10 requests per 10 seconds

#### Response
The API will respond with a list of SHA-1 hashes matching the provided range.
If no hashes match the given range, the response will have a 404 status code.

| Status | MIME             | Type     | Description               |
|--------|------------------|----------|---------------------------|
| 200    | application/json | string[] | A list of breached hashes |
| 404    | application/json | string[] | An empty list             |
| 429    | text/html        | -        | Rate limit exceeded       |
| 400    | application/json | object   | Error message             |

#### Errors
| Code     | Message       | Description                                                                                          |
|----------|---------------|------------------------------------------------------------------------------------------------------|
| 49f5c936 | Invalid range | The hash range provided to the hashes endpoint is not within the allowed range of 5 - 40 characters. |

#### Notes
- In case of a 404 status code, some servers may replace the response with an HTML page.
    For any 404 response, the client can always assume that no hashes match the range.
- Requested range may be logged in server logs as it is part of the URL.



## POST hashes endpoint
Get hashes by the given range.
The upside of a POST request over a GET request is that the requested range will not be logged to server logs.

#### URL
| Path                      | Method | Session required |
|---------------------------|--------|------------------|
| `/api/1.0/service/hashes` | POST   | no               |

#### Arguments
| Arguments | Type   | Default | Required | Description                                                      |
|-----------|--------|---------|----------|------------------------------------------------------------------|
| range     | string | -       | yes      | 5-40 characters of a SHA-1 hash to check against in the database |

#### Restrictions
- Authentication required
- User rate limit: 10 requests per 10 seconds

#### Response
The API will respond with a list of SHA-1 hashes matching the provided range.
If no hashes match the given range, the response will have a 404 status code.

| Status | MIME             | Type     | Description               |
|--------|------------------|----------|---------------------------|
| 200    | application/json | string[] | A list of breached hashes |
| 404    | application/json | string[] | An empty list             |
| 429    | text/html        | -        | Rate limit exceeded       |
| 400    | application/json | object   | Error message             |

#### Errors
| Code     | Message       | Description                                                                                          |
|----------|---------------|------------------------------------------------------------------------------------------------------|
| 49f5c936 | Invalid range | The hash range provided to the hashes endpoint is not within the allowed range of 5 - 40 characters. |

#### Notes
- In case of a 404 status code, some servers may replace the response with an HTML page.
    For any 404 response, the client can always assume that no hashes match the range.

# API Notes
- This API uses the security check service as configured in the app settings.
    Some security check services have limited databases and therefore can't guarantee that a hash is secure if it's not included.
- Lists of breached passwords are updated constantly.
    It is therefore not recommended to cache the response of this API for more than a day.