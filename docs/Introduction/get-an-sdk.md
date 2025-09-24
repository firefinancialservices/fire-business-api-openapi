---
title: Get a client SDK
metadata:
  title: ''
  description: ''
  robots: index
content:
  excerpt: >-
    In order to use the Fire Payments API, you will need access to our OpenAPI
    specification.
privacy:
  view: public
---
> 📘 You can download Fire's OpenAPI specification [here](https://github.com/firefinancialservices/fire-business-api-openapi/blob/master/fire-business-api-v1.yaml).

Fire's API Github is public, allowing you to access our OpenAPI specification and use it to access the Fire Payments API whatever way you need. Once you have the file downloaded, you can use the language you are comfortable with to create a library you can call to embed it into your backend.

***

## Creating a library

Once you've downloaded the OpenAPI file, we have created a few examples below of how to use this to create a library you can call.

This script makes use of the`openapi-client-axios`function in JavaScript. You can use this to create a client that can be used to call every function of the Fire Payments API. This allows you to create scripts that run automatically, or in your command line.

```javascript
const OpenAPIClientAxios = require('openapi-client-axios').default;
const yaml = require('js-yaml');
const fs = require('fs');
const hash = require('hash.js');


// initialise the API Client
const api = new OpenAPIClientAxios({ 
    definition: yaml.load(fs.readFileSync("fire-business-api-v1.yaml", 'utf8')) 
});

api.init()
  .then((client) => {
    apiClient = client
```
