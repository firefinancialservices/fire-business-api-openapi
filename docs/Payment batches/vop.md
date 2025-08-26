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

Currently, when bank transfers are added to a batch and submitted, the batch payments are automatically sent unless approvals are enabled. When VoP comes into effect, the process for creating and processing batches will change. The account holder name assigned to a payee will be checked to see if it matches the name on the account held at the receiving institution. If you have opted in to VoP, you will be able to see the matching response we receive from the receiving institution and define your workflow based on the response.

VoP only affects bank transfer batches in Euro.

<br />

## VoP Responses

There are five possible responses to a VoP check.

<Tabs>
  <Tab title="Full match">
    The account holder name assigned to your payee is an exact match with the name held by the beneficiary account provider.
  </Tab>

  <Tab title="Partial match">
  The account holder name assigned to your payee is not an exact match with the name held by the beneficiary account provider, but they are similar. For example, the account holder name is recorded as 'John Doh', while the receiving institution has the name 'John Doe'.
  </Tab>

  <Tab title="No match">
    The account holder name assigned to your payee is not an exact match with the name held by the beneficiary account provider.
  </Tab>

  <Tab title="Pending">
    Fire is waiting to receive the result of the VoP check from the beneficiary account provider.
  </Tab>

  <Tab title="Unable to match">
    The VoP check was unable to produce a result.
  </Tab>
</Tabs>

By calling our  [Get Batch Details](https://docs.fire.com/reference/getdetailssinglebatch#/) endpoint, you will receive a JSON response summarising the VoP check results by indicating how many of each results have been received. This is useful for summary information on the payees in a large batch. You can also call [List Items for a bank transfer batch](https://docs.fire.com/reference/getitemsbatchbanktransfer#/) to see more detailed information on an individual batch item.

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
```Text List items for a bank tarnsfer batch response
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

<Accordion title="Opt-in/Opt-out criteria" icon="fa-info-circle">
 You cannot opt out of the Verification of Payee check when adding new payees or sending payments through our web portal. Opting out is only allowed for multi-payment batches (i.e., batches containing more than one payment). This section applies only to API applications and batches.
</Accordion>

When creating an API application, you will be required to choose whether to opt in or opt out of the Verification of Payee check. This preference will then apply to all payments made via the API using the associated application keys.

You will be asked to make this selection regardless of whether the application is created through the Fire desktop application or via the Fire Payments API. Any existing applications will default to opt out.

## Submitting large batches

<Tabs>
  <Tab title="Opted in">
If you have opted in to perform a VoP check on batch payments, we will perform the check when a batch item is added to the batch. The check result can take up to 5 seconds to be received from the beneficiary account provider so it will not be included in the response message.  If you would like to check this information, you can call our <a href="https://docs.fire.com/reference/getdetailssinglebatch#/"> Get Batch Details </a> endpoint. This will summarise the results of the check for the payees in the batch.  You can also call [List Items for a bank transfer batch](https://docs.fire.com/reference/getitemsbatchbanktransfer#/) to see more detailed information on an individual batch item.
  </Tab>

  <Tab title="Opted out">
 Opting out of VoP checks is only permissible for multi-payment batches (i.e. batches that contain more than 1 batch item). If you have opted out and the batch contains more than 1 batch item at the point of submission, we will not perform a VoP check on any payment included in the batch.
  </Tab>
</Tabs>

## Single payment batches

Single payment batches do not fall under the opt out exemption for VoP checks. For any batches containing only one payment, a VoP check will be performed. 

If you have opted in, we will perform the check on every batch item as it is added to the batch. You can call our <a href="https://docs.fire.com/reference/getdetailssinglebatch#/"> Get Batch Details </a> endpoint to view the result of this check. 

If you have opted out, we will perform the check at the point the batch is submitted. If the result returned by the beneciairy account provider is a Full Match, the payment will be processed without any need for input from you. If the result is anything other than Full Match, you will receive a push notification displaying the result. You will be required to either accept or reject the result before we will continue to process the batch.