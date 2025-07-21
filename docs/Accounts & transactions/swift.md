---
title: SWIFT accounts
excerpt: >-
  The SWIFT network is a global messaging network allowing members to exchange
  information. It allows Fire customers to receive international payments
  directly to their Fire account.
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
# How it works

SWIFT receiving will allow Fire customers to receive payments in a currency other than GBP or Euro. These will then be converted and sent to your default Fire account. You will have to use your SWIFT account details to receive these payments.

> ❗️ To receive international payments on your Fire account, you will need to request SWIFT account details.

<br />

## Requesting SWIFT Payments

> Your default accounts are the first EUR and GBP accounts that were opened for you. Incoming payments will be credited to your default euro or sterling account, depending on whether you are a Fire-EU or Fire-UK customer. Payments are automatically routed based on currency and your country of incorporation

SWIFT payments can be requested by navigating to your Fire home screen on your default account. You can also request these details on mobile.

![](https://files.readme.io/f4027ca4d53ea3949c5166abf17a64fe4eab77919fb3e54274a9b0ac1051682b-image.png)

<br />

Your SWIFT account information will be displayed alongside your existing BIC and IBAN (for a Euro account)/Sort Code and Account number (for a GBP account). Please note they will be a *separate* BIC and IBAN to your existing Fire account details.

<br />

> You can only have one set of SWIFT account details per Fire account. For example, if you are a Fire-EU user, they will be available on your default euro account.

<br />

## SWIFT and the Fire Payments API

You can also request SWIFT details using the Fire Payments API. The `ican` you use will have to be the `ican` of your default account.