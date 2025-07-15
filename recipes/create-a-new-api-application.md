---
title: Create a new API application
description: >-
  Use this recipe to write a Java script that will help you create a new API
  application on your Fire account.


  Endpoints in this recipe:


  https://api.fire.com/business/v1/apps/accesstokens

  https://api.fire.com/business/v1/apps
hidden: false
recipe:
  color: '#2c4185'
  icon: 🗺️
---
```javascript JavaScript
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

// initialise the API Client, ensure your downloaded version of our OpenAPI file 
//is in the same directory
const api = new OpenAPIClientAxios({ 
    definition: yaml.load(fs.readFileSync("fire-business-api-v1.yaml", 'utf8')) 
});

api.init()
  .then((client) => {
    apiClient = client

    client.authenticate(null, {
      clientId: clientId, 
      clientSecret: clientSecret, 
      refreshToken: refreshToken, 
      nonce: nonce, 
      grantType: "AccessToken"
    }).then(res => { 
      accessToken = res.data.accessToken;
      createApp();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});

// Create Application
const createApp = () => {   
    apiClient.createApiApplication(
		null, 
        {"ican": 12345, 
		 "enabled": true,
		 "expiry": "2019-08-22T07:48:56.460Z",
		 "applicationName": "Javascript Test",
		 "numberOfPaymentApprovalsRequired": null,
		 "numberOfPayeeApprovalsRequired": null,
		"permissions": ["PERM_BUSINESS_GET_ACCOUNT]},
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 
        console.log(res.data);
    })
    .catch(err => {
        console.log(err);
    });
}  
```

```json Response Example
{
  clientId: 'XXXXXX',
  refreshToken: 'XXXXXXX',
  clientKey: 'XXXXXXXXXXX'
}
```

# Load required libraries

<!-- javascript@1-4 -->

These are the libraries you will need to run this code.

OpenAPIClientAxios can generate an API Client directly from the OpenAPI definition.

# Set up some variables and constants

<!-- javascript@6-10 -->

This is where you set your API Token details, and create your nonce and client secret.

# Create the API object and initialise the API client

<!-- javascript@17-24 -->

Provide the OpenAPI spec to the library, then initialise the code to create the API Client object.

# Use the client to get an Access Token

<!-- javascript@25-40 -->

With the API Client created in the previous step, call the authenticate endpoint with the correct data to retrieve your access token.

# Create your new API application

<!-- javascript@42-60 -->

Finally, use the API Client and the access token to call the createApiApplication endpoint.

Use the body to input your application details, and call a result that will reveal your application's details, such as shared key.