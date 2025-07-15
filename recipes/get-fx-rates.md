---
title: Get FX rates
description: >-
  Use this recipe to write a Java script that will help you call the daily FX
  rates for selected currencies.


  Endpoints in this recipe


  https://docs.fire.com/reference/authenticate

  https://docs.fire.com/reference/getfxrates-1
hidden: false
recipe:
  color: '#2c4185'
  icon: 💰
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

// initialise the API Client
const api = new OpenAPIClientAxios({ 
    definition: yaml.load(fs.readFileSync("fire-business-api-v1.yaml", 'utf8')) 
});

api.init()
  .then((client) => {
    apiClient = client
	console.log(apiClient);

    client.authenticate(null, {
      clientId: clientId, 
      clientSecret: clientSecret, 
      refreshToken: refreshToken, 
      nonce: nonce, 
      grantType: "AccessToken"
    }).then(res => { 
	  //console.log(res); 
      accessToken = res.data.accessToken;
      getFX();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});


const getFX = (sellCurrency, buyCurrency) => { 
    apiClient.getFXRates({"sellCurrency": "EUR", "buyCurrency": "GBP"}, null,
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => {
	   console.log("Daily rate" + ":" + res.data.rate4d)
   })
    .catch(err => {
        console.log(err);
    });
}


```

```json Response Example
{
    "provider": "TCC",
    "buyCurrency": "GBP",
    "sellCurrency": "EUR",
    "fixedSide": "SELL",
    "buyAmount": 8608,
    "sellAmount": 10000,
    "rate4d": 8608
}
```

# Load required libraries

<!-- javascript@1-4 -->

These are the libraries you will need to run this code.

OpenAPIClientAxios can generate an API Client directly from the OpenAPI definition.

# Set up some variables and constants

<!-- javascript@6-14 -->

This is where you set your API Token details, and create your nonce and client secret.

# Create the API object and initalise the API client

<!-- javascript@16-24 -->

Provide the OpenAPI spec to the library, then initialise the code to create the API Client object.

# Use the client to get an Access Token

<!-- javascript@26-35 -->

With the API Client created in the previous step, call the authenticate endpoint with the correct data to retrieve your access token. We also initalise our getFX() variable here.

# Get the daily FX rates for your selected currency

<!-- javascript@44-52 -->

Use the API client and the access token to call the getFXRates endpoint.