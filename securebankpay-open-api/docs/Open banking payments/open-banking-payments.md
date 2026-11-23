---
title: Open banking payments
metadata:
  title: Bank Pay open banking payments
  description: Accept account-to-account payments through Bank Pay.
  robots: index
privacy:
  view: public
---

Bank Pay enables merchants to accept account-to-account payments directly from a customer's bank account. The customer selects their bank, gives consent, and authorises the payment in their banking application.

## Payment requests

Each payment begins with a payment request. The request contains the amount, currency, destination account (icanTo), merchant reference, description and return URL.

Call `POST /business/v1/paymentrequests` to create the request. The response contains an eight-character payment request code. Create the customer payment URL using:

```text
https://securebankpay.com/{code}
```

The URL can be presented as a Pay by Bank button, sent by email or SMS, or embedded in another customer journey.

## Hosted payment pages

With hosted payment pages, Bank Pay displays the payment details, bank selection, consent, authorisation hand-off, and response pages. This is the simplest integration model.

The merchant creates the payment request, redirects the customer to the Bank Pay URL, and handles the configured return URL. The merchant should then call `GET /business/v2/payments/{paymentUuid}` to confirm the authoritative payment status.

## Integrated payment pages

With integrated payment pages, the merchant hosts the payment details and bank-selection experience. Use `GET /business/v1/aspsps` to retrieve the available banks when the merchant owns the bank-selection page.

The regulatory consent and authorisation stages remain part of the Bank Pay payment journey. The merchant must still handle the return URL, validate webhooks, and retrieve the final payment status from the API.

## Reference endpoints

- [Create a payment request](/reference/newpaymentrequest)
- [List available banks](/reference/getlistofaspsps)
- [Get payment details](/reference/getpaymentdetailsv2)
- [List payment attempts](/reference/getpaymentrequestpaymentsv2)
- [Request a refund](/reference/bankpayrefundrequest)

Continue with the [payment flow](/docs/payment-flow/payment-flow), [payment status](/docs/payment-flow/payment-status), and [webhook validation](/docs/webhooks/webhook-validation) guides.
