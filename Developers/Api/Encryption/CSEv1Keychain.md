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

After the keychain string has been decoded, it needs to be separated into the salt and the payload.
The salt are the first `crypto_pwhash_SALTBYTES` bytes of the keychain string.
The payload comes after the first `crypto_pwhash_SALTBYTES` bytes.

With the salt from the keychain string and the users master password, the decryption key can be computed using [`crypto_pwhash`](https://download.libsodium.org/doc/password_hashing/default_phf#example-1-key-derivation).
The key length is `crypto_box_SEEDBYTES`.
The password is the master password.
The salt is the salt from the keychain string with the length `crypto_pwhash_SALTBYTES`.
The ops limit is `crypto_pwhash_OPSLIMIT_INTERACTIVE`.
The mem limit is `crypto_pwhash_MEMLIMIT_INTERACTIVE`.
The algorithm is `crypto_pwhash_ALG_ARGON2ID13` which is currently `crypto_pwhash_ALG_DEFAULT`.

Now the payload needs to be split into the nonce and the cipher text.
The nonce are the first `crypto_secretbox_NONCEBYTES` bytes of the payload.
The cipher text comes after the first `crypto_secretbox_NONCEBYTES` bytes of the payload.

With the cipher text, the nonce and the decryption key, [`crypto_secretbox_open_easy`](https://download.libsodium.org/doc/secret-key_cryptography/secretbox#example) can be used to decrypt the keychain.
The cipher text is used for `c`, the nonce is `n` and decryption key is `k`.

The result is now a JSON encoded string representing the actual keychain object.
The JSON object contains the property `keys` which contains an object representing all the keys in the keychain.
The name of each property in `keys` is the id of the key and the value is the key as [hexadecimal](https://download.libsodium.org/doc/helpers#hexadecimal-encoding-decoding) encoded string.
Each key needs to be decoded before it can be used for encryption.


### Encrypt the keychain
The master password is required to encrypt the keychain.
It must be at least 12 and no more than 128 characters long.

**Important:** Always generate a new salt when encrypting the keychain and never re-use previously used salts.
