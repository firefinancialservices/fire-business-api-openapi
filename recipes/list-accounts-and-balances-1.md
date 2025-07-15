---
title: List Accounts and Balances
description: >-
  Use this recipe to write a Java script that will help you call a list of all
  the accounts under your Fire main account and their balances. This can be
  useful to generate reports for yourself or your users.


  Endpoints in this recipe


  https://docs.fire.com/reference/authenticate

  https://docs.fire.com/reference/getaccounts
hidden: false
recipe:
  color: '#2c4185'
  icon: 🌐
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
    definition: yaml.load(fs.readFileSync("./fire-business-api-v1.yaml", 'utf8')) 
});

api.init()
  .then((client) => {
    apiClient = client;

    client.authenticate(null, {
      clientId: clientId, 
      clientSecret: clientSecret, 
      refreshToken: refreshToken, 
      nonce: nonce, 
      grantType: "AccessToken"
    }).then(res => { 
      accessToken = res.data.accessToken;
      listAccounts();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});

// list accounts and balances
const listAccounts = () => {   
    apiClient.getAccounts(
        null, 
        null, 
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => {
        //console.log(res.data);
        res.data.accounts.forEach((account) => {
            console.log(account.ican + " " + account.name + ": " + (account.balance/100).toLocaleString('en', {minimumFractionDigits: 2}) + account.currency.code);
        });
    })
    .catch(err => {
        console.log(err);
    });
}  

```

```json Response Example
1232 Main Account: 20.38EUR
3455 Sterling Account: 19.07GBP
```

# Load required libraries

<!-- javascript@1-4 -->

These are the libraries you will need to run this code. 

OpenAPIClientAxios can generate an API Client directly from the OpenAPI definition.

# Set up some variables and constants

<!-- javascript@6-14 -->

This is where you set your API Token details, and create your nonce and client secret.

# Create the API object and initiatise the API Client

<!-- javascript@16-23 -->

Provide the OpenAPI spec to the library, then initialise the code to create the API Client object.

# Use the client to get an Access Token

<!-- javascript@25-38 -->

With the API Client created in the previous step, call the authenticate endpoint with the correct data to retrieve your access token.

# Get the list of accounts

<!-- javascript@33,41-56 -->

Finally, use the API Client and the access token to call the getAccounts endpoint. 

Loop over the accounts and print out the details.