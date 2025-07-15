---
title: List Transactions
description: >-
  Use this recipe to write a Java script that will help you call a list of all
  the accounts under your Fire main account, find their ican and list all your
  Fire account's transactions. This can be useful to generate reports for
  yourself or your users.


  Endpoints in this recipe


  https://docs.fire.com/reference/authenticate

  https://docs.fire.com/reference/getaccounts

  https://docs.fire.com/reference/gettransactionsbyaccountidv3
hidden: false
recipe:
  color: '#2c4185'
  icon: 🧭
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
      getAccountInfo();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});




//Initalise an ican array [] and call the api to store each ican associated with your Fire account
const getAccountInfo = () => {   
    apiClient.getAccounts(null,  null,
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 
	   let ican = [];
       res.data.accounts.forEach((account) => {
       if(account.ican){
			ican.push(account.ican);
			listTransactions(account.ican);
	   }
	   });
	 //console.log(ican);
	//you can also note each ican individually, but storing it allows us to call each accounts transactions
   })
    .catch(err => {
        console.log(err);
    });
}

 
// list Transactions
	const listTransactions = (ican) => {  
	apiClient.getTransactionsByAccountIdv3(
		{"ican": ican}, 
			null,
		{ headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 

     res.data.content.forEach((transaction) => {
      console.log(transaction.txnId + ":" + " " +  transaction.amountBeforeCharges);
	   });
    })
   .catch(err => {
        console.log(err);
    });
}


```

```json Response Example
12654081: 1
12654079: 1
12648058: 1
12590400: 100
12331751: 1
11729577: 500
10859123: 1000
```

# Load required libraries

<!-- javascript@1-4 -->

These are the libraries you will need to run this code.

OpenAPIClientAxios can generate an API Client directly from the OpenAPI definition.

# Set up some variables and constants

<!-- javascript@7-15 -->

This is where you set your API Token details, and create your nonce and client secret.

# Create the API object and initiatise the API Client

<!-- javascript@16-24 -->

Provide the OpenAPI spec to the library, then initialise the code to create the API Client object.

# Use the client to get an Access Token

<!-- javascript@26-35 -->

With the API Client created in the previous step, call the authenticate endpoint with the correct data to retrieve your access token.

# Call and store each ican associated with your fire account

<!-- javascript@47-55 -->

Call the getAccounts endpoint to store each endpoint. If you only want an individual ican, you can return the results of this, and note the index of that ican to store it as a singular variable. This script will return every transaction across all your Fire accounts.

# Call the getTransactionsByAccountIdV3 endpoint



Use the ican to call this endpoint.