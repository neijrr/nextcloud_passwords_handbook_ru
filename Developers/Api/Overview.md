### Api Version Scheme
The api follows this version scheme: `MAJOR.MINOR`.
A major version makes incompatible api changes.
A minor version adds new features.
Bugfixes and security fixes are not visible over the api.
Support for an old version of the api will be ended by a new major version of the app.

##### Special note for the initial release
The version 1.0 api is not complete at this point. It will be so by the beginning of 2019.

### API version support
| API | Introduced | Removed |
| --- | --- | --- |
| 0.1 | 2018.1 | 2020.1 |
| 1.0 | 2018.1 | - |

### General Notes
 - The api does not guarantee the order of the properties of an api object
 - Not supported arguments for api actions are silently discarded
 - If a versionable api object is changed in any way, a new revision is created
 - UUIDs follow the [UUID V4 Schema according to RFC 4122](https://wikipedia.org/wiki/Universally_Unique_Identifier)