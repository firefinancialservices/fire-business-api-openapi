---
title: Authentication
excerpt: 
category: 5f6fc3cc6768a5003ca89038
slug: authentication
---
Access to the API is by Bearer Tokens. You will need to set up set up a Fire Application to access the Fire API. 

To do this:

1. Sign In at https://business.fire.com.
1. Select the **Settings** tab.
1. Select the **API** section.
1. Click **Add New Application**.

![Creating a new Application](https://www.fire.com/wp-content/uploads/2023/05/settings-api.png)

Give your API Application a name, and select the required permissions.

![Selecting Permissions](https://www.fire.com/wp-content/uploads/2023/05/settings-api-new.png)

If you have selected permissions relating to batch processing, you can configure how many approvers are need prior to processing a batch. There are 2 types of approvals:

1. **Approvals for adding a new payee for a batch** – in line with legislation, you are required to approve new payees on your account using Strong Customer Authentication (SCA). The first time you make a payment to a payee, Fire will send notifications to Full Users so they can approve. This will be a single notification containing the details of all the new payees in the batch. Once a payee has been approved on your account, it is not necessary to approve payments going forward (although you can can opt to approve all payments – see below).
1. **Approvals for batches of bank transfers** – you can set this to 0 to automatically process batch payments to previously approved payees. This is useful for setting up unattended automated batch payments.

You can also have multiple approvers if you want for either type to enhance security. All full users will get a push notification to approve to their linked mobile devices to approve the batch.

Once you’ve finished above, click “Create“, and take note of your Client ID, Client Key and Refresh Token – the Client Key will not be displayed again.

> 🚧 
> 
> If you ever accidentally reveal the Client Key (or accidentally commit it to Github for instance) it is vital that you log into firework online and delete/recreate the App Tokens as soon as possible. Anyone who has these three pieces of data can access the API to view your data and set up payments from your account (depending on the scope of the tokens).

## Authentication
You now use these pieces of data to retrieve a short-term Access Token which you can use to access the API. This will be set as the Bearer Token in the `Authorization` header for all API calls. For security reasons, the Access Token expires within a relatively short timeframe – there is a 15 minute window to use it.

In order to create an Access Token, you require:

* **Client ID** – The app’s Client ID created above.
* **Refresh Token** – The app’s Refresh Token created above.
* **Nonce** – A random non-repeating number (that is incremented from the previously used value) used as a salt for the clientSecret below. The simplest nonce is a unix time.
* **Client Secret** – A Client Secret is the a SHA256 sum of the nonce concatenated with the Client Key.

It will be possible to create a SHA256 hash using your coding language or choice. For testing, you can the following shell command:

```bash
echo -n $NONCE$CLIENT_KEY | sha256sum
```

Now call the [Access Token](/reference/authenticate) endpoint to send send a POST request containing the following JSON:

```JSON
{ 
  "refreshToken": "<REFRESH_TOKEN>", 
  "clientId": "<CLIENT_ID>", 
  "nonce": "92376214646124", 
  "clientSecret": "<CLIENT_SECRET>", 
  "grantType": "AccessToken" 
}
```

You will receive an Access Token and details of the allowed permissions in response:

```JSON
{ 
  "businessId": 23416, 
  "apiApplicationId": 113423, 
  "expiry":"2021-10-22T07:48:56.460Z", 
  "permissions": [ "PERM_BUSINESSES_GET_SERVICES", "PERM_BUSINESSES_GET_ACCOUNTS", "PERM_BUSINESSES_GET_ACCOUNT", "PERM_BUSINESSES_GET_ACCOUNT_TRANSACTIONS", "PERM_BUSINESSES_GET_ACCOUNT_TRANSACTIONS_FILTER", "PERM_BUSINESSES_GET_FUNDING_SOURCES", "PERM_BUSINESSES_GET_FUNDING_SOURCE", "PERM_BUSINESSES_GET_FUNDING_SOURCE_TRANSACTIONS", "PERM_BUSINESSES_GET_WEBHOOKS", "PERM_BUSINESSES_GET_WEBHOOK_EVENT_TEST", "PERM_BUSINESSES_GET_LIMITS", "PERM_BUSINESSES_GET_FX_RATE", "PERM_BUSINESSES_GET_APPS", "PERM_BUSINESSES_GET_APP_PERMISSIONS", "PERM_BUSINESSES_GET_APPS_PERMISSIONS", "PERM_BUSINESSES_GET_WEBHOOK_TOKENS" ], 
  "accessToken": "<ACCESS_TOKEN>" 
}
```

Once you have the access token, pass it as a header for every API call, like so:

```HTTP
Authorization: Bearer $ACCESS_TOKEN
```

Whenever it expires, create a new nonce and get a new access token again. You can have multiple access tokens active at the same time if you have, for instance, multiple servers. 
