---
title: Get started with batches
excerpt: >-
  Transfer funds into your Fire account for automatic distribution to employees
  or contractors.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Why use Fire to make batch payments?

[block:html]
{
  "html": "<div style=\"display: flex;\">\n  <div style=\"flex: 1; height: 280px; align-items: center; justify-content: center;\">\n    <div><img src=\"https://www.fire.com/_next/image/?url=https%3A%2F%2Fsiteapi.fire.com%2Fwp-content%2Fuploads%2F2024%2F06%2Fpayments-use-case-1.png&w=1920&q=75\" width=\"350\"></div>\n    <div style=\"padding: 12px 32px\"><a href=\"https://docs.fire.com/docs/accounts-1#how-can-you-use-fire-to-submit-batch-payments\" style=\"color: #2C4185; text-decoration: none; font-weight: bold;\">Send batch payments</a></div>\n    <div style=\"padding: 0px 32px; width: 350px;\">Apply your own logic to manage and split funds. Initiate payouts via the Fire Payments API.</div>\n  </div>\n\n  <div style=\"flex: 1; height: 280px; align-items: center; justify-content: center;\">\n    <div><img src=\"https://www.fire.com/_next/image/?url=https%3A%2F%2Fsiteapi.fire.com%2Fwp-content%2Fuploads%2F2024%2F06%2FDebit-use-case-3.png&w=1920&q=75\" width=\"350\"></div>\n    <div style=\"padding: 12px 32px\"><a href=\"https://docs.fire.com/docs/accounts-1#how-can-you-use-fire-to-submit-batch-payments\" style=\"color: #2C4185; text-decoration: none; font-weight: bold;\">View batch details</a></div>\n    <div style=\"padding: 0px 32px; width: 350px;\">Manage unlimited account reconciliations, get instant payment notifications, set custom user access, and transfer money instantly between Fire accounts.</div>\n  </div>"
}
[/block]


<br />

Find more use cases and examples on [Fire's website](https://www.fire.com/services/payment-and-accounts/).

***

## How can you use Fire to submit batch payments?

> 📘 See the Batches reference section for more detailed information.

<br />

Use our API to create, manage and send batch payments (processing multiple payment transactions as a single group or batch), eliminating manual fund distribution. You can also split payments using batches, and process refunds. Individual batches are identified by the `batchUuid` attribute, which you can find by calling 'List all Batches' first. Individual payments within batches are identified by the `itemUuid`.

[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e506d778df3a95cb05143997c6d2764b8cfff1d6a3fc36b380c997d80a0c104e-mermaid-diagram-2025-06-18-093752.png",
        "",
        "Bank Transfer Batch Payment Sequence Diagram"
      ],
      "align": "center",
      "border": true,
      "caption": "Bank Transfer Batch Payment Sequence Diagram"
    }
  ]
}
[/block]


If you want to practice using the batch payments API endpoints listed below, Fire has recipes created in Javascript to see how to use the API to do things like call a list of your accounts. To use these, you'll need our OpenAPI definition document, which you can download from our Github [here.](https://github.com/firefinancialservices/fire-business-api-openapi). You can use these endpoints to start creating batches, and to generate reports on them. 

Fire allows the creation of 3 main batch types:

- Bank Transfer batches - contain payments to other financial institutions in the UK and Ireland, or external Fire accounts
- Internal Transfer batches - contain payments to your other Fire accounts
- International Transfer batches - contain payments to be distributed outside of the UK and Ireland. These batches must be paid to existing payees

If you are adding payments to a batch, they must be the correct type for the batch they are being added to. All payments in a batch must be the same currency. New payee batches are created for you once you submit the batch, and are specifically to approve any new payees in an existing batch for users with approvals enabled. You can find more on payees below.

<br />

The first step for any batch type is to create a batch and save the ` batchUuid`  returned. If you have already created the batch, you can find this by listing all your batches.

- [Create a new batch](https://docs.fire.com/reference/createbatchpayment)
- [List all batches](https://docs.fire.com/reference/getbatches)

<br />

Next, you should add all the payments to your batch using the ` batchUuid`. The type of payment you can add depends on the type. Save the `itemUuid` for these payments. If you want to view any of these payments, you can find this by calling the details of this batch. If you would like to remove a payment after adding it, you can. Please note, any new payees will need to be approved, and you can view who these payees are using the 'List Items for a New Payee Batch' endpoint.

<br />

_Bank Transfer batches:_

- [Add a bank transfer to a batch](https://docs.fire.com/reference/addbanktransferbatchpayment)
- [List items for a bank transfer batch](https://docs.fire.com/reference/getitemsbatchbanktransfer)
- [Remove a bank transfer from a batch](https://docs.fire.com/reference/deletebanktransferbatchpayment)

<br />

_Internal Transfer batches:_

- [Add an internal transfer to a batch](https://docs.fire.com/reference/addinternaltransferbatchpayment)
- [List items for an internal transfer batch](https://docs.fire.com/reference/getitemsbatchinternaltrasnfer)
- [Remove an internal transfer from a batch](https://docs.fire.com/reference/deleteinternaltransferbatchpayment)

<br />

_International Transfer batches:_

- [Add an international transfer to a batch](https://docs.fire.com/reference/addinternationaltransferbatchpayment-1)
- [List items for an international transfer batch](https://docs.fire.com/reference/getitemsbatchinternationaltransfer-1)
- [Remove an international transfer from a batch](https://docs.fire.com/reference/deleteinternationaltransferbatchpayment-1)

<br />

_Batch Details_

- [Get the details of a batch](https://docs.fire.com/reference/getdetailssinglebatch)
- [List approvals for a batch](https://docs.fire.com/reference/getlistofapproversforbatch)

<br />

Finally, once you have added your payments and are happy with it, you can submit your batch. Once it is submitted, you will need to approve any new payees if you have payee approval enabled. If you decide not to use this batch, you can cancel it. You cannot cancel a batch once it is submitted and approved.

- [Submit a batch](https://docs.fire.com/reference/submitbatch)
- [Cancel a batch](https://docs.fire.com/reference/cancelbatchpayment)

<br />

_Payees_

Verification of Payee (VoP) is a mandatory service for SEPA payments aimed at preventing misdirected and fraudulent payments by confirming that the payee's name matches the provided bank account details (IBAN). For Euro payment batches, from October 2025, any new payee will have to be approved, irrespective of if approvals are enabled or not.

- [List items for a new payee batch](https://docs.fire.com/reference/getnewpayeebatch)

_See how to write a script to use these endpoints here_

[block:tutorial-tile]
{
  "backgroundColor": "#001188",
  "emoji": "🦉",
  "id": "67ed4b66db8fc00030f8dde7",
  "link": "https://docs.fire.com/v2.0/recipes/automate-your-payouts-with-batches",
  "slug": "automate-your-payouts-with-batches",
  "title": "Automate your payouts with batches"
}
[/block]


<br />

***

<br />

Fire customers use our API to submit large batch payments, which ensures swift reconciliation to identify payees and automate payouts, thus avoiding manual errors. For example, [JustTip](https://www.fire.com/case-studies/automated-large-volume-batch-payments-to-distribute-tips/) has automated large volume batch payments to all employees across partner facilities, handling over 2000 payments in a short time.