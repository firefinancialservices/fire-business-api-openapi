---
title: Refunds
metadata:
  title: Bank Pay refunds
  description: Request a refund for a Bank Pay payment.
  robots: index
privacy:
  view: public
---

Call `POST /business/v1/payments/{paymentUuid}/bankpayrefund` for a payment that is eligible for refund.

Provide the refund amount, currency, merchant reference, description, reason, and merchant number where applicable. The response contains a refund request UUID and status.

Refund statuses include `REJECTED` and `RECEIVED`.
