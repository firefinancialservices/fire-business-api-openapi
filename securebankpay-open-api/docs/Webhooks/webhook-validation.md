---
title: Webhook validation
metadata:
  title: Validate Bank Pay webhooks
  description: Verify signed Bank Pay webhook notifications.
  robots: index
privacy:
  view: public
---

Bank Pay webhook notifications are sent as signed JWTs with content type `application/jwt`.

1. Read the JWT header and extract the `kid` value.
2. Load the matching public key from the Bank Pay JWKS endpoint supplied for your environment.
3. Verify the JWT signature, issuer, audience, expiry, and claims before processing the event.
4. Process events idempotently because delivery may be retried.
5. Return HTTP 200 only after the notification has been accepted.

Use the payment UUID in the event to retrieve the current payment state. The API remains the source of truth for payment status.
