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

Currently, when you add bank transfer payments to a batch and submit this, the batch payments will be automatically sent unless you have approvals enabled. When VoP comes into affect, the way batches are created and processed will change. Fire will need to confirm that the name you assign a payee, matches the name on the account you are sending the payment to in the receiving institution.

VoP only affects bank transfer batches in Euro.

<br />

## VoP Responses

There are five possible responses to a VoP check.

<Tabs>
  <Tab title="Full match">
    The name on the account matches the name you gave the payee completely.
  </Tab>

  <Tab title="Partial match">
    The name om the account does not match the name you gave the payee completely, but they are similar. For example, you assigned the payee name as "John Doe", where the receiving institution has the name "John Dome".
  </Tab>

  <Tab title="No match">
    The name on the account does not match the name you gave the payee.
  </Tab>

  <Tab title="Pending">
    Fire is waiting to receive the result of the VoP check.
  </Tab>

  <Tab title="Unable to match">
    The VoP check was unable to produce a result.
  </Tab>
</Tabs>

## Creating API applications

<Accordion title="Opt-in/Opt-out criteria" icon="fa-info-circle">
  Please note that you cannot opt-out of the Verification of Payee check for the addition of new payees to your account manually. Any opt-out is only permitted for batch payments. This section is only relevant to API applications and batches.
</Accordion>

Verification of Payee will act on an opt-in basis for API applications with Fire.

When you create an API application you will now be asked to opt in or opt-out of a verification of payee check when you create the application. This will then apply to any payments made via the API using those application keys.

You will need to opt-in/opt-out whether you create your application on the Fire desktop application or via the Fire Payments API.

## Submitting large batches

<Tabs>
  <Tab title="Opted in">
    If you have opted in to complete a VoP check on any new payees, all payees submitted in the batch will be verified to ensure the name you have submitted for that payee matches the name on the recieving account. If you would like to check this information, you can call our <a href="https://docs.fire.com/reference/getdetailssinglebatch#/"> Get Batch Details </a> endpoint. This will summarise the results of the check for the payees in the batch. Please note it is not recommended to opt-in for large batches.
  </Tab>

  <Tab title="Opted out">
    If you have opted out, your payees (including new payees) will not be verified provided your batch does not only contains a single payment.
  </Tab>
</Tabs>

## Single payment batches

Unfortunately, any single payment batches do not fall under the exemption for large batches. For any batches only containing one payment, payees will be verified regardless. If you have opted-in, you can call our <a href="https://docs.fire.com/reference/getdetailssinglebatch#/"> Get Batch Details </a> endpoint to view the result of this check. If you have opted out, you will receive a push notification only if the verification returns a response that is not a full name match against the receiving account.