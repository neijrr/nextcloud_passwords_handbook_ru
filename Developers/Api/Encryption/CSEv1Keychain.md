### How it works
The CSEv1 keychain is an encrypted string which contains a JSON object with the keys used for the client side encryption.

The CSEv1 keychain is implemented using [libsodium](https://download.libsodium.org/doc/bindings_for_other_languages).
You can find the default implementation of the CSEv1 keychain [in the passwords-client package](https://git.mdns.eu/nextcloud/passwords-client/blob/master/src/Encryption/Keychain/CSEv1Keychain.js).


### Structure
This structure describes the decrypted keychain. Not the encrypted string.

| Property | Type | Description |
| --- | --- | --- |
| `keys` | Object | A list with the keys. The identifier is an UUID v4 and the value is the key as [hexadecimal](https://download.libsodium.org/doc/helpers#hexadecimal-encoding-decoding) encoded string. |
| `current` | string | The UUID of the latest key which should be used for encryption. |


### Decrypt the keychain
The master password is required to decrypt the keychain.
It must be at least 12 and no more than 128 characters long.
The encrypted keychain is stored as a [hexadecimal](https://download.libsodium.org/doc/helpers#hexadecimal-encoding-decoding) encoded string and needs to be decoded before it can be decrypted.

**Important:** Prior to Passwords 2020.2.0 the encrypted keychain string was encoded with [base64](https://download.libsodium.org/doc/helpers#base64-encoding-decoding).
Users who set up CSE before the official release may have a base64 encoded keychain which should be taken into account.

After the keychain string has been decoded, it needs to be separated into the salt and the text.
The salt are the first `crypto_pwhash_SALTBYTES` bytes of the keychain string.
The text comes after the first `crypto_pwhash_SALTBYTES` bytes.

Now, the decryption key for the keychain can be computed.