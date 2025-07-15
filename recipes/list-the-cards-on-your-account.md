---
title: List the cards on your account
description: >-
  Use this recipe to write a Java script that will help you call a list of all
  the cards issued under your Fire account. This can be useful for generating
  reports and managing your cards.


  Endpoints in this recipe:

  https://api.fire.com/business/v1/apps/accesstokens

  https://docs.fire.com/reference/getlistofcards
hidden: false
recipe:
  color: '#2c4185'
  icon: 💳
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
      getCards();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});




//List cards
const getCards = () => {   
    apiClient.getListofCards(null, null,
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 
	   res.data.cards.forEach((card) => {
      console.log(card.cardId);
	   });
   })
    .catch(err => {
        console.log(err);
    });
}

```

```json Response Example
12345
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

# Call the list of cards on your account

<!-- javascript@47-58 -->

Finally, use the API Client and the access token to call the getListOfCards endpoint.