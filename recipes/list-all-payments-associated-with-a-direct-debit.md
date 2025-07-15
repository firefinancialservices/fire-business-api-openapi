---
title: List all payments associated with a Direct Debit
description: >-
  Use this recipe to write a Java script that will help you to view the number
  of payments made for a direct debit mandate. This can be useful to track the
  payments made against a specific mandate for reporting.


  Endpoints in this recipe


  https://docs.fire.com/reference/authenticate

  https://docs.fire.com/reference/getdirectdebitmandates

  https://docs.fire.com/reference/getdirectdebitsformandateuuid
hidden: false
recipe:
  color: '#2c4185'
  icon: 💻
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
	//  console.log(res); 
      accessToken = res.data.accessToken;
      getDirectDebitMandates();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});




//Initalise an mandate array [] and call the api to store each mandateUUID associated with your Fire account
const getDirectDebitMandates = () => {   
    apiClient.getDirectDebitMandates(null,  null,
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 
	   //console.log(res);
	   let mandateUuid = [];
       res.data.mandates.forEach((mandate) => {
       if(mandate.mandateUuid){
			mandateUuid.push(mandate.mandateUuid);
			getDirectDebitsForMandateUuid(mandate.mandateUuid);
	   }
	   });
   })
    .catch(err => {
        console.log(err);
    });
}

 //call the direct debits associated with that mandate
	const getDirectDebitsForMandateUuid = (mandateUuid) => {
			console.log(mandateUuid);
	apiClient.getDirectDebitsForMandateUuid(
		{"mandateUuid": mandateUuid}, 
			null,
		{ headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 
	res.data.directDebits.forEach((directDebit) => {
      console.log(directDebit.directDebitUuid);
	   });
    })
   .catch(err => {
        console.log(err);
    });
}

```

```json Response Example
1a2b3c4d-XXXX-YYYY-ZZZZ-ABCD12345678
1a2b3c4d-XXXX-YYYY-ZZZZ-ABCD12345678

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

With the API Client created in the previous step, call the authenticate endpoint with the correct data to retrieve your access token. We also initalise our getDirectDebitMandates() variable here.

# Create an array to store your mandate UUIDs

<!-- javascript@47-56 -->

Use the API client and access token to call the getDirectDebitMandates() endpoint. 

A mandate is the permission provided to your bank by you to charge the direct debit. With your Fire account, you need a mandate UUID to find the payments associated with this permission.

# List all payments associated with that Direct Debit

<!-- javascript@66-74 -->

Using your stored mandate UUIDs, call the getDirectDebitsForMandateUuid function to see the corresponding direct debit payments under that mandate.