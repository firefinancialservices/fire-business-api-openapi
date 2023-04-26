---
title: Authentication
excerpt: 
category: 5f6fc3cc6768a5003ca89038
slug: authentication
---
Access to the API is by Bearer Tokens. 

You must first log into the [firework online application](https://business.fire.com) and create a new Application in the **Settings > API** page. (You will need your PIN digits and 2-Factor Authentication device).

Give your application a Name and select the scope/permissions you need the application to have (more on Scopes below).

You will be provided with three pieces of information - the **App Refresh Token**, **Client ID **and **Client Key**. You need to take note of the Client Key when it is displayed - it will not be shown again.

You now use these pieces of data to retrieve a short-term** Access Token** which you can use to access the API. The Access Token expires within a relatively short time, so even if it is compromised, the attacker will not have long to use it. The Client Key is the most important piece of information to keep secret. This should only ever be stored on a backend server, and never in a front end client or mobile app.

> 🚧 
> 
> If you ever accidentally reveal the Client Key (or accidentally commit it to Github for instance) it is vital that you log into firework online and delete/recreate the App Tokens as soon as possible. Anyone who has these three pieces of data can access the API to view your data and set up payments from your account (depending on the scope of the tokens).

Once you have the access token, pass it as a header for every call, like so:

```http
Authorization: Bearer $ACCESS_TOKEN
```



Whenever it expires, create a new nonce and get a new access token again.