---
title: Verification of Payee
excerpt: >-
  Verification of Payee (VoP) will come into affect in October 2025. This page
  summarises the impacts and effects for users of the Fire Payments API.
deprecated: false
hidden: true
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> Verification of Payee (VoP) is a mandatory service for SEPA payments aimed at preventing misdirected and fraudulent payments by confirming that the payee's name matches the provided bank account details (IBAN).

Currently, when you add bank transfer payments to a batch and submit this, the batch payments will be automatically sent unless you have approvals enabled. When VoP comes into affect, the way batches are created and processed will change.

VoP only affects bank transfer batches in Euro.

## Creating API applications

<Accordion title="Opt-in/Opt-out criteria" icon="fa-info-circle">
  Please note that you cannot opt-out of the Verification of Payee check for the addition of new payees to your account manually. Any opt-out is only permitted for large batch payments (i.e. batches containing more than one payment). This section is only relevant to API applications and batches.
</Accordion>

Verification of Payee will act on an opt-in basis for API applications.

When you create an API application you will now be asked to opt in or opt-out of a verification of payee check when you create the application. This will then apply to any payments made via the API using those application keys.

You will need to opt-in/opt-out whether you create your application on the Fire desktop application or via the Fire Payments API.

## Submitting large batches

<Tabs>
  <Tab title="Opted in">
    If you have opted in to complete a VoP check on any new payees, all payees submitted in the batch will have to be checked and verified by you. This will be enabled in the same way as batch approvals, via push notification on your mobile device. Please note this is not recommended for large batches, as each payee approval must be individually completed.
  </Tab>

  <Tab title="Opted out">
    If you have opted out, your payees (including new payees) will not be verified provided your batch contains more than one payment.
  </Tab>
</Tabs>

## Single Payment Batches

Unfortunately, any single payment batches do not fall under the exemption for large batches. For any batches only containing one payment, this payee will have to be verified via a mobile push notification.