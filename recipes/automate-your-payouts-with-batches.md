---
title: Automate your payouts with batches
description: >-
  Use this recipe to write a Java script that will help you create and submit
  batch payments with Fire. This can be useful to payout multiple users at once,
  or set up a loop for recurring large payouts. You could also process refunds
  in this way.


  Endpoints in this recipe:


  https://docs.fire.com/reference/createbatchpayment

  https://docs.fire.com/reference/addbanktransferbatchpayment

  https://docs.fire.com/reference/submitbatch
hidden: false
recipe:
  color: '#001188'
  icon: 🦉
---
```javascript JavaScript
const OpenAPIClientAxios = require('openapi-client-axios').default;
const yaml = require('js-yaml');
const fs = require('fs');
const hash = require('hash.js');

// set up constants and variables
let apiClient;
const clientId = "clientId";
const clientKey = "clientKey";
const refreshToken = "refreshToken";

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
      createBatch();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});

// Create batch container to hold your payments
const createBatch = () => {   
    apiClient.createBatchPayment(
        null, 
        {"type": "BANK_TRANSFER", //in this example, we are creating and submitting a bank transfer batch
		 "currency": "EUR",
		 "batchName": "Javascript Test",
		 "jobNumber": "1234optional"
		}, 
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => {
       // console.log(res.data);
		batchUuid = res.data.batchUuid;
		return Promise.all([
			addPayment(batchUuid, 67204, 368722, "PAYEE_ID", 50, "JS test", "JS Test")
		]);
	})
		.then(()=>{
			return submitBatch();
        }).catch(err => {
        console.log(err);
    });
}  

//Add payments to your created batch

const addPayment = (batchUuid, icanFrom, payeeId, payeeType, amount, myRef, yourRef) => {
	return apiClient.addBankTransferBatchPayment({"batchUuid": batchUuid} , {
  "icanFrom": icanFrom,
  "payeeId": payeeId,
  "payeeType": payeeType,
  "amount": amount,
  "myRef": myRef,
  "yourRef": yourRef
	}, { headers: { "Authorization": "Bearer " + accessToken }} 
	).then(res => {
		console.log(res.data);
		
	}).catch(err => {
        console.log(err);
	});
}

//Submit your batch
const submitBatch = () => {
	console.log("wtf");
	apiClient.submitBatch({"batchUuid": batchUuid}, null, { headers: { "Authorization": "Bearer " + accessToken }} 
	).then(res => {
		console.log(res.data);
	}).catch(err => {
        console.log(err);
	});
}

```

```json Response Example
201
```

# Load required libraries

<!-- javascript@1-4 -->

These are the libraries you will need to run this code.

OpenAPIClientAxios can generate an API Client directly from the OpenAPI definition.

# Set up some variables and constants

<!-- javascript@7-10 -->

This is where you set your API Token details, and create your nonce and client secret.

# Create the API object and initalise the API client

<!-- javascript@17-23 -->

Provide the OpenAPI spec to the library, then initialise the code to create the API Client object.

# Use the client to get an Access Token

<!-- javascript@26-33 -->

With the API Client created in the previous step, call the authenticate endpoint with the correct data to retrieve your access token. We also initalise our createBatch() variable here.

# Create a batch container to hold your payments

<!-- javascript@43-56 -->

Calling our createBatch() variable by making it equal to the operationID for the function to call the createBatchPayment() endpoint. Set our batchUuid as a variable. Initalise our addPayments() variable. Promise and .then() ensures our functions run sequentially versus asynchronously

# Add payments to your batch.

<!-- javascript@67-76 -->

Calling our addPaymenst() variable by making it equal to the operationID for the function to call the addInternalTransferBatchPayment() endpoint. You can change this to be bank transfers or international payments, and add as many payments as needed to your JSON body. Initalise your submitBatch() variable.

# Submit your batch.

<!-- javascript@85-91 -->

Calling our submitBatch() variable by making it equal to the operationID for the function to call the submitBatch() endpoint. Your payments will now be submitted and processed