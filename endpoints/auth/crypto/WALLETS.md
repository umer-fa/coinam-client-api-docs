[&laquo; Return to main page](../../../README.md)

# Wallets

* List all existing wallets
* Create a new wallet

## List all wallets
##### `GET`  [/auth/crypto/wallets]()

### Request Params

Param | Type | Required | Description
--- | --- | --- | ---
xsrf | hash32 | yes | XSRF token
coin | string | yes | Crypto-currency code (2-8 alphanumeric digits)

### Success Response

Param | Type |  Description
--- | --- | --- 
count | integer | Number of coins available to users
coin | [**`object` Coin**](../../../models/CRYPTO.md#object-coin) | Coin object
protocol | object | See [**`object` Protocol**](../../../models/CRYPTO.md#object-protocol)
wallets | array | Indexed array of `Wallet` objects. (See [**`object` Wallet**](../../../models/CRYPTO.md#object-wallet)).

### Errors

Code | Description| Possible Resolution
--- | --- | ---

* It is also possible to get one of [**Global Error Messages**](../../../README.md#global-error-messages).

## Create a new wallet
##### `POST`  [/auth/crypto/wallets?create_new]()

### Request Params

Param | Type | Required | Description
--- | --- | --- | ---
xsrf | hash32 | yes | XSRF token
coin | string | yes | Crypto-currency code (2-8 alphanumeric digits)
newLabel | string | yes | A name/label for new wallet (maximum 32 characters)
type | string | **depends** | If a selection is available under `walletsTypes` prop in [**`object` Protocol**](../../../models/CRYPTO.md#object-protocol) then it is required
recoveryOpt | string | **depends** | Recovery option, required if one or more option is available under "recoveryOpts" prop in [**`object` CryptoWalletsType**](../../../models/CRYPTO.md#object-cryptowalletstype)
recoveryKeysPassword | string | **depends** | A password for encryption of wallet private key(s)
recoveryCustodyPartner | string | **depends** | If recovery option is `custody` then ID of custody partner
recoveryPubKey | string | **depends** | If recovery option is `multiSigSelf` then a public key 

### Success Response

Param | Type |  Description
--- | --- | --- 
wallet | string | New wallet identifier (36 byte)

### Errors

Code | Description| Possible Resolution
--- | --- | ---
`LABEL_REQ` | Wallet label param is required | n/a
`LABEL_LEN` | Wallet label length must be between 3 and 32 digits | n/a
`LABEL_INVALID` | Wallet label contains an illegal character | n/a
`WALLET_TYPE_REQ` | Wallet type selection is required | n/a
`WALLET_TYPE_INVALID` | Selected wallet type is not a valid option | n/a
`RECOVERY_OPT_REQ` | Recovery option is required | n/a
`RECOVERY_OPT_INVALID` | Selected recovery option is invalid | n/a
`RECOVERY_PASSWORD_REQ` | Recovery keys encryption password is required | n/a
`RECOVERY_PASSWORD_INVALID` | Recovery keys encryption contains an illegal character | n/a
`RECOVERY_PASSWORD_LEN` | Recovery keys encryption contains an illegal character | n/a
`CRYPTO_WALLETS_NA` | Wallets of said crypto are not available to this user | n/a
`CRYPTO_WALLETS_LIMIT` | User has reached limit of maximum wallets allowed in said crypto | Check "limit" and "count" params in response

* It is also possible to get one of [**Global Error Messages**](../../../README.md#global-error-messages).