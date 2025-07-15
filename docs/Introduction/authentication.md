---
title: Authentication
excerpt: >-
  Once you have a library set-up, you'll need to authenticate your application
  information.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
Access to the API is by bearer tokens. You'll need your API application information to generate this.

## Generate your bearer token

With your API application information, you now use these pieces of data to retrieve a short-term Access Token which you can use to access the API. This will be set as the Bearer Token in the `Authorization` header for all API calls. For security reasons, the Access Token expires within a relatively short timeframe – there is a 15 minute window to use it.

In order to create an Access Token, you require:

- **Client ID** – The app’s Client ID.
- **Refresh Token** – The app’s Refresh Token.
- **Nonce** – A random non-repeating number (that is incremented from the previously used value) used as a salt for the clientSecret below. The simplest nonce is a unix time.
- **Client Secret** – A Client Secret is a SHA256 sum of the nonce concatenated with the Client Key.

It will be possible to create a SHA256 hash using your coding language of choice. For testing, you can the following shell command:

```bash
echo -n $NONCE$CLIENT_KEY | sha256sum
```

Now call the [Access Token](/reference/authenticate) endpoint to send send a POST request containing the following JSON:

```JSON
{ 
  "refreshToken": "<REFRESH_TOKEN>", 
  "clientId": "<CLIENT_ID>", 
  "nonce": "92376214646124", 
  "clientSecret": "<CLIENT_SECRET>", 
  "grantType": "AccessToken" 
}
```

You will receive an Access Token and details of the allowed permissions in response:

```JSON
{ 
  "businessId": 23416, 
  "apiApplicationId": 113423, 
  "expiry":"2021-10-22T07:48:56.460Z", 
  "permissions": [ "PERM_BUSINESSES_GET_SERVICES", "PERM_BUSINESSES_GET_ACCOUNTS", "PERM_BUSINESSES_GET_ACCOUNT", "PERM_BUSINESSES_GET_ACCOUNT_TRANSACTIONS", "PERM_BUSINESSES_GET_ACCOUNT_TRANSACTIONS_FILTER", "PERM_BUSINESSES_GET_FUNDING_SOURCES", "PERM_BUSINESSES_GET_FUNDING_SOURCE", "PERM_BUSINESSES_GET_FUNDING_SOURCE_TRANSACTIONS", "PERM_BUSINESSES_GET_WEBHOOKS", "PERM_BUSINESSES_GET_WEBHOOK_EVENT_TEST", "PERM_BUSINESSES_GET_LIMITS", "PERM_BUSINESSES_GET_FX_RATE", "PERM_BUSINESSES_GET_APPS", "PERM_BUSINESSES_GET_APP_PERMISSIONS", "PERM_BUSINESSES_GET_APPS_PERMISSIONS", "PERM_BUSINESSES_GET_WEBHOOK_TOKENS" ], 
  "accessToken": "<ACCESS_TOKEN>" 
}
```

Once you have the access token, pass it as a header for every API call, like so:

```HTTP
Authorization: Bearer $ACCESS_TOKEN
```

Whenever it expires, create a new nonce and get a new access token again. You can have multiple access tokens active at the same time if you have, for instance, multiple servers.

***

## Using a library

If you have downloaded Fire's OpenAPI definition, you can create a script to generate your access token. For example:

```javascript
const OpenAPIClientAxios = require('openapi-client-axios').default;
const yaml = require('js-yaml');
const fs = require('fs');
const hash = require('hash.js');

// set up constants and variables
let apiClient;
const clientId = "<clientId>";
const clientKey = "<clientKey>";
const refreshToken = "<refreshToken>";

let accessToken;
const nonce = Math.floor(new Date().getTime()/1000.0);
const clientSecret = hash.sha256().update(nonce + clientKey).digest('hex');

// initialise the API Client
const api = new OpenAPIClientAxios({ 
    definition: yaml.load(fs.readFileSync("fire-business-api-v1.yaml", 'utf8')) 
});

api.init()
  .then((client) => {
    apiClient = client
	//console.log(apiClient);

    client.authenticate(null, {
      clientId: clientId, 
      clientSecret: clientSecret, 
      refreshToken: refreshToken, 
      nonce: nonce, 
      grantType: "AccessToken"
    }).then(res => { 
	  //console.log(res); 
      accessToken = res.data.accessToken;
```