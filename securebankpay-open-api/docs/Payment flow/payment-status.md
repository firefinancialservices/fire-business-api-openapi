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

Bank Pay payment responses may include a `to` object with `type: BANK_PAY_ACCOUNT`. Its account details are represented by `id`, `alias`, `nsc`, and `accountNumber`. The Bank Pay response does not expose additional account fields such as `bic` or `iban`.

Important statuses include:

- `AWAITING_AUTHORISATION`: the customer has started the authorisation journey.
- `AWAITING_AUTHORISATION`: some business accounts require dual authorisation for payments
- `NOT_AUTHORISED`: the payment was cancelled, rejected, or failed.
- `PENDING`: the bank is carrying out further checks.
- `AUTHORISED`: the payment has been successfully initiated.
- `FUNDS_CONFIRMED`: funds have been received and will be applied.
- `SETTLED`: funds have been applied to the destination account.

Use `GET /business/v2/paymentrequests/{paymentRequestCode}/payments` to retrieve all attempts for a payment request.
