---
title: List all users
description: >-
  Use this recipe to write a Java script that will help you list all the users
  on you Fire account. This can be useful to identify a specific users UserID
  for transaction monitoring.


  Endpoints in this recipe:


  https://docs.fire.com/reference/authenticate

  https://docs.fire.com/reference/getusers
hidden: false
recipe:
  color: '#2c4185'
  icon: 🤸‍♂️
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
      getUsers();

    }).catch(err => {
      console.log(err);
      console.log("Could not get API client");
    });
	});


const getUsers = () => {   
    apiClient.getUsers(null,  null,
        { headers: { "Authorization": "Bearer " + accessToken }}
    ).then(res => { 
	   res.data.users.forEach((user) => {
       console.log("Name" + ":" + user.firstName + " " +  "UserID" + ": " + user.id); //you can edit this output to see your desired information
	   });   
   })
    .catch(err => {
        console.log(err);
    });
}

 

```

```json Response Example
Name:Jane Doe UserID: 123456
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

With the API Client created in the previous step, call the authenticate endpoint with the correct data to retrieve your access token.

# List all the users on your Fire account

<!-- javascript@44-54 -->

Call the getUsers() function to list all the users on your fire account.