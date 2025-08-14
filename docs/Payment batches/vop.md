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
  Please note that you cannot opt-out of the Verification of Payee check for the addition of new payees to your account manually. Any opt-out is only permitted for large batch payments. This section is only relevant to API applications and batches.
</Accordion>

/

Verification of Payee will act on an opt-in basis for API applications.

When you create an API application you will now be asked to opt in o

## Submitting large batches

## Single Payment Batches