---
title: Webhooks
excerpt: Webhooks allow you to be notified of events as they happen on your fire.com accounts. This is useful if you have systems that need to know when things happen on your account, such as payments or withdrawals.
category: 5f6fc3cc6768a5003ca89038
slug: webhooks
---
A webhook is a URL that you set up on your backend. We can then send the details of various events to you at this URL as they happen. You can have many webhooks and can configure each one to listen for different events in fire.com.

## Configuring your webhook settings

You can set up webhooks in the [firework business application](https://business.fire.com). There are a set of Webhook API Tokens in the **Profile > Webhooks** section. The key ID (kid) in the JWT header will be the webhooks public token, and you should use the corresponding private token as the secret to verify the signature on the JWT.

## Designing your webhook processing

In general, webhooks do not guarantee data integrity, as communication or errors on the sender/receiver side can occur. To address these potential issues, both the sender and the receiver applications need to provide for idempotency. Idempotency ensures that an operation can be executed "at least once" and "at most once", resulting in the same outcome each time.

To implement idempotency on the sender side, retrying failed webhook requests might be necessary to ensure that the operation is executed "at least once", and our system is designed to automatically retry failed requests three to five times, with a one-minute interval between each attempt.

To achieve idempotency on your, the receiver side, you need to ensure the "at most once" principle by disregarding duplicates. This can be done by enforcing a unique constraint on the payload data, such as Txn_id.

## Receiving a webhook at your server

You will receive an array of events as they occur. In general, there will be only one event per message, but as your volume increases, we will gather all events in a short time-window into one call to your webhook. This reduces the load on your server.

When the data is sent to your webhook endpoint it will be signed and encoded using JWT (JSON Web Token). JWT is a compact URL-safe means of representing data to be transferred between two parties (see [JWT.io](https://jwt.io) for more details and to get a code library for your programming environment). The signature is created using a shared secret that only you and fire.com have access to, so you can be sure that it came from us.

A JWT looks like this:

```text
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0TY3ODkwI...ibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9.TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```



This needs to be decoded using the library from JWT.io. You should ensure that the signature is valid by checking the HS256 signature included in the JWT was created using the private token corresponding to the key ID (kid) in the header.