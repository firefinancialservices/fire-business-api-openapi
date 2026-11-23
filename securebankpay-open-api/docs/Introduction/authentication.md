---
title: Authentication
metadata:
  title: Bank Pay authentication
  description: Generate bearer tokens for Bank Pay API calls.
  robots: index
privacy:
  view: public
---

Bank Pay uses bearer access tokens. Tokens expire after 15 minutes.

Create a client secret by hashing the nonce and Client Key:

```bash
echo -n "$NONCE$CLIENT_KEY" | sha256sum
```

Call `POST /business/v1/apps/accesstokens` with the Client ID, Refresh Token, nonce, generated client secret, and `grantType: AccessToken`.

Use the returned token on subsequent calls:

```http
Authorization: Bearer ACCESS_TOKEN
```

The application must be granted the permissions required by the endpoints it calls, including `PERM_BUSINESS_POST_PAYMENT_REQUEST`, `PERM_BUSINESS_GET_ASPSPS`, `PERM_BUSINESS_GET_PAYMENT`, and `PERM_BUSINESS_GET_PAYMENT_REQUEST_PAYMENTS`.
