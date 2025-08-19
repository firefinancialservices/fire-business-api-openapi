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

Currently, when bank transfer payments are added to a batch and submitted, the batch payments are automatically sent unless approvals are enabled. When VoP comes into effect, the process for creating and processing batches will change. The name assigned to a payee will need to match the name on the account held at the receiving institution.

VoP only affects bank transfer batches in euro.

<br />

## VoP Responses

There are five possible responses to a VoP check.

<Tabs>
  <Tab title="Full match">
    The name on the account matches completely the name assigned to the payee.
  </Tab>

  <Tab title="Partial match">
    The name on the account does not completely match the name assigned to the payee, but they are similar. For example, the payee name is recorded as 'John Doe', while the receiving institution has the name 'John Dome'.
  </Tab>

  <Tab title="No match">
    The name on the account does not match the name assigned to the payee.
  </Tab>

  <Tab title="Pending">
    Fire is waiting to receive the result of the VoP check.
  </Tab>

  <Tab title="Unable to match">
    The VoP check was unable to produce a result.
  </Tab>
</Tabs>

By calling our  [Get Batch Details](https://docs.fire.com/reference/getdetailssinglebatch#/) endpoint, you will receive a JSON response for each payee in a batch, with one of the above results. This is useful for summarising information on the payees in a large batch. You can also call [List Items for a bank transfer batch](https://docs.fire.com/reference/getitemsbatchbanktransfer#/) to see more detailed information on a singular payee check.

```json Get Batch Details response
{
  "batchUuid": "F2AF3F2B-4406-4199-B249-B354F2CC6019",
  "type": "BANK_TRANSFER",
  "status": "COMPLETE",
  "sourceName": "Payment API",
  "batchName": "January 2018 Payroll",
  "jobNumber": "2018-01-PR",
  "callbackUrl": "https://my.webserver.com/cb/payroll",
  "currency": "EUR, GBP, USD",
  "numberOfItemsSubmitted": 1,
  "valueOfItemsSubmitted": 10000,
  "numberOfItemsFailed": 0,
  "valueOfItemsFailed": 0,
  "numberOfItemsSucceeded": 1,
  "valueOfItemsSucceeded": 10000,
  "lastUpdated": "2021-04-04T10:48:53.540Z",
  "dateCreated": "2021-04-04T10:48:53.540Z"
  "payeeChecks" [
    "countFullMatch": 1,
    "countPartialMatch": 1,
    "countNoMatch": 1,
    "countUnableToMatch": 1,
    "countPending": 1
    ]

```
```json List items for a bank transfer batch response
{
  "total": 1,
  "items": [
    {
      "batchItemUuid": "F2AF3F2B-4406-4199-B249-B354F2CC6019",
      "status": "PENDING_APPROVAL",
      "result": {
        "code": 500001,
        "message": "SUCCESS"
      },
      "dateCreated": "2021-04-04T10:48:53.540Z",
      "lastUpdated": "2021-04-04T10:48:53.540Z",
      "icanFrom": 2150,
      "amount": 10000,
      "myRef": "Testing a transfer via batch",
      "yourRef": "Testing a transfer via batch",
      "refId": 123782,
      "payeeType": "ACCOUNT_DETAILS",
      "payeeId": 1234567,
      "destIban": "IE63CPAYXXXXXXX792562",
      "destAccountHolerName": "John Doe",
      "payeeCheckStatus": "PARTIAL_MATCH"
      "payeeCheckPartialMatchName": "John Dome"
    } 
  ]
    "pagination": {
      "total_entries": 2,
      "total_pages": 1,
      "current_page": 1,
      "per_page": 25,
      "previous_page": -1,
      "next_page": -1,
      "order": "created_at",
      "order_asc_desc": "asc"
    }
}

```

<br />

## Creating API applications

<Accordion title="Opt in/Opt out criteria" icon="fa-info-circle">
  Please note that you cannot opt out of the Verification of Payee check for the addition of new payees to your account manually. Any opt out is only permitted for batch payments. This section is only relevant to API applications and batches.
</Accordion>

Verification of Payee will act on an opt in basis for API applications with Fire.

When you create an API application you will now be asked to opt in or opt out of a verification of payee check when you create the application. This will then apply to any payments made via the API using those application keys.

You will need to opt in or opt out whether you create your application on the Fire desktop application or via the Fire Payments API.

## Submitting large batches

<Tabs>
  <Tab title="Opted in">
    If you have opted in to complete a VoP check on any new payees, all payees submitted in the batch will be verified to ensure the name submitted for each payee matches the name on the receiving account. If you would like to check this information, you can call our <a href="https://docs.fire.com/reference/getdetailssinglebatch#/"> Get Batch Details </a> endpoint. This will summarise the results of the check for the payees in the batch. Please note it is not recommended to opt in for large batches.
  </Tab>

  <Tab title="Opted out">
    If you have opted out, payees (including new payees) will not be verified provided your batch does not only contains a single payment.
  </Tab>
</Tabs>

## Single payment batches

Unfortunately, any single payment batches do not fall under the exemption for large batches. For any batches only containing one payment, payees will be verified regardless. If you have opted in, you can call our [Get batch details](\[https://docs.fire.com/reference/getdetailssinglebatch#/]\(https://docs.fire.com/reference/getdetailssinglebatch#/\)) endpoint to view the result of this check. If you have opted out, you will receive a push notification only if the verification returns a response that is not a full match against the receiving account.