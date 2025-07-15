---
title: Create a payment request
description: >-
  Use this recipe to write a Java script that will help you create a payment
  request. This can be useful to get paid quickly via open banking.


  Endpoints in this recipe


  https://docs.fire.com/reference/authenticate

  https://docs.fire.com/reference/newpaymentrequest
hidden: false
recipe:
  color: '#2c4185'
  icon: 🤝
---
```javascript JavaScript
const yaml = require('js-yaml');
const fs = require('fs');
const hash = require('hash.js');

// set up constants and variables
let apiClient;
const clientId = "<clientId>;
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
      createPaymentRequest();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});





const createPaymentRequest = () => {   
    apiClient.newPaymentRequest(null,  {"currency": "EUR", "type": "OTHER", "icanTo": <ican>,"amount": 100, "myRef": "Test", 
	"description": "test", "maxNumberPayments": 1},
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 
	   console.log("Payment request code" + ": " + res.data.code);
   })
    .catch(err => {
        console.log(err);
    });
}

```

```json Response Example
{
    "type": "OTHER",
    "code": "abcde7ab"
}
```

# Load required libraries

<!-- javascript@1-4 -->

These are the libraries you will need to run this code.

OpenAPIClientAxios can generate an API Client directly from the OpenAPI definition.

# Set up some variables and constants

<!-- javascript@7-14 -->

This is where you set your API Token details, and create your nonce and client secret.

# Create the API object and initalise the API client

<!-- javascript@17-24 -->

Provide the OpenAPI spec to the library, then initialise the code to create the API Client object.

# Use the client to get an Access Token

<!-- javascript@26-35 -->

With the API Client created in the previous step, call the authenticate endpoint with the correct data to retrieve your access token. We also initalise our createPaymentRequest() variable here.

# Create your payment request

<!-- javascript@47-56 -->

Use the client and access token to call newPaymentRequest with your chosen information for the payment request.