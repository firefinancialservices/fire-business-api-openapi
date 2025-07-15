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

> Your default accounts are the first EUR and GBP accounts that were opened for you. These accounts are automatically used for receiving international payments in their respective currencies.

SWIFT payments can be requested by navigating to your Fire home screen, and selecting account information. You can also request these details on mobile.

**design mockup, to be replaced**

<Image align="center" width="75% " src="https://files.readme.io/0a8c944f55a894ebf4a7d875ce07836f51606c4ce93f5655baf3fcafb3d5d429-image.png" />

Your SWIFT account information will be displayed alongside your existing BIC and IBAN (for a Euro account)/Sort Code and Account number (for a GBP account). Please note they will be a *separate* BIC and IBAN to your existing Fire account details. 

<br />

> You can only have one set of SWIFT account details per Fire account. For example, if you request these details on your Euro account, you will not be able to request them on your GBP account.

<br />

## SWIFT and the Fire Payments API

You can also request SWIFT details using the Fire Payments API. The `ican` you use will have to be the `ican` of your default account.
