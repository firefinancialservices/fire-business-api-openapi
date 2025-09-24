---
title: Get started with webhooks
metadata:
  title: ''
  description: ''
  robots: index
content:
  excerpt: >-
    Fire offers webhooks that provide real-time notifications on events,
    enabling you to trigger specific API actions such as automatically
    transferring funds across accounts based on predefined rules.
privacy:
  view: public
---
> 📘 Webhooks allow you to be notified of events as they happen on your Fire accounts. This is useful if you have systems that need to know when things happen on your account, such as payments or withdrawals.

## Setting up and testing your webhooks

> *A webhook is a URL that you set up on your backend. We can then send the details of various events to you at this URL as they happen. You can have as many webhooks as you like and can configure each one to watch out for different events on your Fire account.*

<br />

1. You can set up webhooks in the [Fire for Business web application](https://business.fire.com). There are a set of Webhook API Tokens in the **Profile > Webhooks** section. The key ID (kid) in the JWT header will be the webhooks public token, and you should use the corresponding private token as the secret to verify the signature on the JWT. 

<br />

<Image align="center" className="border" border={true} src="https://files.readme.io/5a840e984cc760ab658f89f51a363d106298f50db8e77cf6a95ad0168e06edc2-image.png" />

<br />

2. Use a website like [webhook.site](https://webhook.site/) to test your webhooks, by setting a webhook up with the URL they provide.
3. Select 'Test' on where your webhooks are listed in the web application.

<Image align="center" className="border" border={true} src="https://files.readme.io/87a5278bdd7998c2face11e9fb285dc2d6b907643f6d626d1eb1f4c92f24c016-image.png" />

4. You will see the response on  [webhook.site](https://webhook.site/)

<Image align="center" className="border" border={true} src="https://files.readme.io/4462049db314e7aea853350fa529756cb93ded5893ade73c23b64765cfca1509-image.png" />

<br />

5. Decode it on a site like [jwt.io](jwt.io)

<Image align="center" className="border" border={true} src="https://files.readme.io/72098e5d83a862f99fe08591818332b689495c0e58e9e719db40782929aa6221-image.png" />

<br />

***

<br />

## Designing your webhook processing

Webhooks don’t always guarantee that data is delivered correctly, because there can be problems when sending or receiving information. To handle these issues, both the sending and receiving applications (such as yours) need to ensure that actions are completed properly.

This means that when a webhook is sent, it should be designed to allow retries if something goes wrong, ensuring the event is processed at least once. Our system automatically tries to resend failed requests three to five times, waiting one minute between each attempt.

On the receiving side, ensure that handling multiple instances of the same webhook doesn’t cause any issues. This can be achieved by using unique identifiers in the data, so if the same message is received again, it can be ignored. You can test this functionality on [webhook.site](webhook.site).

***

<br />

## Receiving a webhook at your server

When events occur, they will be sent to your server as an array. In general, there will be only one event per message, but as your volume increases, we will gather all events in a short time-window into one call to your webhook. This reduces the load on your server.

When the data is sent to your webhook endpoint it will be signed and encoded using JWT (JSON Web Token). JWT is a compact URL-safe means of representing data to be transferred between two parties (see [JWT.io](https://jwt.io) for more details and to get a code library for your programming environment). The signature is created using a shared secret that only you and Fire have access to, so you can be sure that it came from us.

A JWT looks like this:

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0TY3ODkwI...ibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

This needs to be decoded using the library from JWT.io. You should ensure that the signature is valid by checking the HS256 signature included in the JWT was created using the private token corresponding to the key ID (kid) in the header.

Again, you can see this in action on [webhook.site](webhook), before you actually embed it into into your own URL.

***

## Fire Webhooks

Fire offers webhook notifications for the following event types:

* Account Created
* Card Created
* Card Authorisation
* Card Settlement
* Lodgment Received
* Payment Request Payment Received
* Fire Open Payment Authorised
* Fire Open Payment Lodgment Received

<br />

For real-time information if you are using an authorisation endpoint, use our API to get full information on the card or payment.

## Updating and viewing your applications/webhooks.

Using the Fire Payments API, you can now call various endpoints to send a test webhook, list webhook tokens and list all webhooks you have created. You can also view your created API applications, their permissions, and update them as needed.

* [Create an API application](https://docs.fire.com/reference/createapiapplication)
* [List all API applications](https://docs.fire.com/reference/getapiapplications-1)
* [List all permissions for an API application](https://docs.fire.com/reference/getpermissions-1)
* [List all permissions for API applications](https://docs.fire.com/reference/getallpermissions-1)
* [Send test webhooks](https://docs.fire.com/reference/sendtestwebhook-1)
* [List all webhooks](https://docs.fire.com/reference/getwebhookevents)

<br />

*See how to write a script to use these endpoints here*

<TutorialTile backgroundColor="#2c4185" emoji="🗺️" id="67f65477b8a44600390f07a3" link="https://docs.fire.com/v2.0/recipes/create-a-new-api-application" slug="create-a-new-api-application" title="Create a new API application" />

<br />

***

<br />

Fire customers use our webhooks to act alongside our API to create event-triggered applications to solve specific problems. For example, [MyMilkMan ](https://www.fire.com/case-studies/automating-payouts-to-milk-distributors/)use webhooks to notify them when funds from their acquiring partners arrive in their account, and then use the Fire Payments API to distribute those payments to milk distributors.
