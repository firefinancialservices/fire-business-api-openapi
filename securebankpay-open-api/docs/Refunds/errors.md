---
title: Errors
metadata:
  title: Bank Pay errors
  description: Handle Bank Pay API errors.
  robots: index
privacy:
  view: public
---

Errors are returned as an object containing an `errors` array. Each error includes a numeric `code` and a human-readable `message`.

For `401` and `403` responses, verify that the bearer token is present, valid, unexpired, and has the permission required by the endpoint. For `400` responses, validate the request body, identifiers, currency, and payment-request state.
