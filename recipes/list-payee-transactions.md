---
title: List Payee Transactions
description: >-
  Use this recipe to write a Java script that will help you call a list of all
  the Payee IDs under your Fire account and find the transactions associated
  with them. This can be useful to pull information on a specific business that
  is always paid out in a large, multi payee batch payment.


  Endpoints in this recipe


  https://docs.fire.com/reference/authenticate

  https://docs.fire.com/reference/getpayees

  https://docs.fire.com/reference/getpayeetransactions
hidden: false
recipe:
  color: '#2c4185'
  icon: 🗯️
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
      getPayeeInfo();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});




//Initalise an id array [] and call the api to store each payeeID associated with your Fire account
const getPayeeInfo = () => {   
    apiClient.getPayees(null,  null,
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 
	   //console.log(res);
	   let id = [];
       res.data.fundingSources.forEach((Payee) => {
       if(Payee.id){
			//console.log(Payee.id)
			id.push(Payee.id);
			getPayeeTransactions(Payee.id);
	   }
	   });
   })
    .catch(err => {
        console.log(err);
    });
}

 //Call the Payee transactons endpoint, this will return all your transactions by Payee unless a specific ID is passed
	const getPayeeTransactions = (id) => {
		//	console.log(id);
	apiClient.getPayeeTransactions(
		{"payeeId": id}, 
			null,
		{ headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 
		console.log("transactionsForPayeeID" + id);
     res.data.transactions.forEach((transaction) => {
      console.log(transaction.txnId + ":" + " " +  transaction.amountBeforeCharges);
	   });
    })
   .catch(err => {
        console.log(err);
    });
}

```

```json Response Example
transactionsForPayeeID123456
123456: 1000

```

# Load required libraries

<!-- javascript@1-4 -->

These are the libraries you will need to run this code.

OpenAPIClientAxios can generate an API Client directly from the OpenAPI definition.

# Set up some variables and constants

<!-- javascript@7-14 -->

This is where you set your API Token details, and create your nonce and client secret.

# Create the API object and initalise the API client

<!-- javascript@17-23 -->

Provide the OpenAPI spec to the library, then initialise the code to create the API Client object.

# Use the client to get an Access Token

<!-- javascript@26-34 -->

With the API Client created in the previous step, call the authenticate endpoint with the correct data to retrieve your access token.

# Initalise an array to store your Payee IDs

<!-- javascript@47-63 -->

In order to get transactions broken down by payee, we first need to call and store our payee IDs. This calls the getPayees() operation from our openAPI file.

# Call the payee transactions endpoint using your stored payee IDs

<!-- javascript@69-82 -->

This now passes your stored payee IDs as a header to call the getPayeeTransactions endpoint.