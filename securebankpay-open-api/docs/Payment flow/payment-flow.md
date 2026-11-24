---
title: Payment flow
metadata:
  title: Bank Pay payment flow
  description: Create and complete an account-to-account payment.
  robots: index
privacy:
  view: public
---

## Create the payment request

Call `POST /business/v1/paymentrequests` with the amount, currency, destination account, merchant reference, description, expiry, and return URL.

The response contains an eight-character `code`. Redirect the customer to:

```text
https://securebankpay.com/{code}
```

## Customer journey

The customer reviews the payment, selects their bank, consents to the payment, and authorises it in their banking app.

If you host the bank-selection screen yourself, call `GET /business/v1/aspsps` first. Otherwise, use the hosted Bank Pay journey.

## Return handling

The return URL can indicate cancellation or include the `paymentUUID` for a payment attempt. Treat the return URL as a signal only and retrieve the authoritative payment status through the API.
