---
title: Payment status
metadata:
  title: Bank Pay payment status
  description: Understand payment lifecycle statuses.
  robots: index
privacy:
  view: public
---

Use `GET /business/v2/payments/{paymentUuid}` to retrieve payment details.

Important statuses include:

- `AWAITING_AUTHORISATION`: the customer has started the authorisation journey.
- `NOT_AUTHORISED`: the payment was cancelled, rejected, or failed.
- `PENDING`: the bank is carrying out further checks.
- `AUTHORISED`: the payment has been successfully initiated.
- `FUNDS_CONFIRMED`: funds have been received and are being applied.
- `SETTLED`: funds have been applied to the destination account.

Use `GET /business/v2/paymentrequests/{paymentRequestCode}/payments` to retrieve all attempts for a payment request.
