---
title: Get started with Bank Pay
metadata:
  title: Bank Pay integration
  description: Integrate Bank Pay open banking payments.
  robots: index
privacy:
  view: public
---

Bank Pay lets merchants accept account-to-account payments from their customers' bank accounts.

The normal integration sequence is:

1. Create an API application with the required Bank Pay permissions.
2. Generate a short-lived bearer token.
3. Create a payment request.
4. Redirect the customer to `https://securebankpay.com/{code}`.
5. Handle the return URL and/or webhook notification.
6. Retrieve payment details until the payment reaches the required status.

Fire is the regulated TSP providing the underlying payment service.
