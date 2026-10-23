---
title: Receive SWIFT payments
metadata:
  title: ''
  description: ''
  robots: index
content:
  excerpt: >-
    The SWIFT network is a global messaging network allowing members to exchange
    information. It enables Fire customers to receive international payments
    directly to their Fire account.
privacy:
  view: public
---
# How it works

SWIFT receiving will allow Fire customers to receive payments in a currency other than euro or sterling. These will then be converted and sent to your default Fire account. You will have to use your SWIFT account details to receive these payments.

> ❗️ To receive international payments on your Fire account, you will need to request SWIFT account details.

<br />

## Requesting SWIFT Payments

> Your default accounts are the first euro and sterling accounts that were opened for you. Incoming payments will be credited to your default euro or sterling account, depending on whether you are a Fire-EU or Fire-UK customer. Payments are automatically routed based on currency and your country of incorporation.

SWIFT payments can be requested by navigating to your default account landing screen on the Fire desktop application. You can also request these details the Fire business mobile application.

![](https://files.readme.io/f4027ca4d53ea3949c5166abf17a64fe4eab77919fb3e54274a9b0ac1051682b-image.png)

<br />

Your SWIFT account information will be displayed alongside your existing BIC and IBAN (for a euro account)/sort code and account number (for a sterling account). These details are different from your existing local account details used for SEPA (euro) and Faster Payments (sterling) transfers, and are specifically designed for cross-border payments via the SWIFT network

<br />

> SWIFT account details can only be requested for your default Fire account. For example, if you are a Fire-EU user, you can request them for your default euro account.

<br />

## SWIFT and the Fire Payments API

You can also request SWIFT details using the Fire Payments API. The `ican` you use will have to be the `ican` of your default account.
