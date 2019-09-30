# Coinam Client API Docs

Coinam Client API documentation.

## Basics

**Base URL:** https://api.coinam.com/client/  
**Charset:** All are from **ASCII** (from dec 32 to 126), unless other charset is mentioned specifically;  


## Endpoints

├── Endpoints  
│   ├── `GET` [**/init_session**](endpoints/INIT_SESSION.md#get-init_session) *(Initiate a new session)*  
│   ├── `GET` [**/session**](endpoints/SESSION.md) *(Get information about current session)*  
│   ├── `GET` [**/countries**](endpoints/COUNTRIES.md) *(Get list of countries)*  
│   ├── `POST` [**/register**](endpoints/REGISTER.md) *(Signup / Registration of new user)*  
│   └── `POST` [**/login**](endpoints/LOGIN.md) *(Authenticate session as a registered user)*  
└── 

## XHR Requests

### Headers

Header | Description
--- | ---
Coinam-Client-Token | Required for all endpoints except [**init_session**](endpoints/INIT_SESSION.md#get-init_session) endpoint
Coinam-Client-Timestamp | Timestamp in UTC (GMT+0:00) timezone

* Params can be sent as `application/json` or `application/x-www-form-urlencoded`
* Response is always sent as `application/json; charset=utf8`

## Global Response Params

Param | Type | Description
--- | --- | ---
`status` | boolean | Determines if request was successful; On `false` response object MAY include `error` param
`error` | string | An error message/code, included in response if there is an error; Can sometimes be an empty string or NULL;

## Global Error Messages

Code | Meaning | Possible Resolution
--- | --- | ---
`DB_CONNECTION_ERROR` | App fails to connect with appropriate API logs database | n/a
`BAD_REMOTE_ADDR` | App fails to determine remote IP address | n/a
`API_SESSION_NOT_FOUND` | No such API session found with given token (and/or in rare cases IP address) | n/a
`API_SESSION_RETRIEVE_ERROR` | There was an error while retrieving API session | Discard existing session; Start  a new one
`SESSION_CHECKSUM_FAIL` | Session checksum validation has failed | Discard existing session; Start a new one
`SESSION_CREATE_ERROR` | Failed to start a new API session | n/a
`SESSION_CREATE_TIMEOUT` | Request new sessions/tokens too fast from same IP address | Possible abuse detected
`XSRF_ERROR` | XSRF/CSRF error | n/a