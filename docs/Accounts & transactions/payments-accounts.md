---
title: Get started with accounts
excerpt: >-
  After creating your Fire account with the help of our sales team and
  integrating with our API, you can start reviewing your account details and
  create recurring payments.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Why use Fire for your payments?

<br />

<HTMLBlock>{`
<div style="display: flex;">
  <div style="flex: 1; height: 280px; align-items: center; justify-content: center;">
    <div><img src="https://www.fire.com/_next/image/?url=https%3A%2F%2Fsiteapi.fire.com%2Fwp-content%2Fuploads%2F2024%2F06%2Fpayments-use-case-3.png&w=1920&q=75" width="260"></div>
    <div style="padding: 12px 32px"><a href="https://docs.fire.com/docs/payments-accounts#accounts-and-transactions" style="color: #2C4185; text-decoration: none; font-weight: bold;">Open multiple accounts</a></div>
    <div style="padding: 0px 32px; width: 250px;">Open additional subaccounts with unique account details in real time, based on events like customer or employee onboarding.</div>
  </div>

  <div style="flex: 1; height: 280px; align-items: center; justify-content: center;">
    <div><img src="https://www.fire.com/_next/image/?url=https%3A%2F%2Fsiteapi.fire.com%2Fwp-content%2Fuploads%2F2024%2F06%2Fpayments-use-case-2.png&w=1920&q=75" width="260"></div>
    <div style="padding: 12px 32px"><a href="https://docs.fire.com/docs/payments-accounts#payees" style="color: #2C4185; text-decoration: none; font-weight: bold;">Manage payees</a></div>
    <div style="padding: 0px 32px; width: 250px;">Fire ensures swift reconciliation to identify payees and automate payouts, thus avoiding manual errors.</div>
  </div>

  <div style="flex: 1; height: 280px; align-items: center; justify-content: center;">
    <div><img src="https://www.fire.com/_next/image/?url=https%3A%2F%2Fsiteapi.fire.com%2Fwp-content%2Fuploads%2F2024%2F06%2FDebit-use-case-1.png&w=1920&q=75" width="260"></div>
    <div style="padding: 12px 32px"><a href="https://docs.fire.com/docs/payments-accounts#direct-debits" style="color: #2C4185; text-decoration: none; font-weight: bold;">Control direct debits</a></div>
    <div style="padding: 0px 32px; width: 250px;">Reduce reconciliation processing times, and manual tasks. Fire helps you to automate payouts based on your own business logic</div>
  </div>
</div>
`}</HTMLBlock>

<br />

Find more use cases and examples on [Fire's website](https://www.fire.com/services/payment-and-accounts/).

***

## What can the Fire Payments API do for you?

> 📘 As part of our payments and accounts product offering, you can use our API to perform actions relating to your accounts, transactions, direct debits and payees. See the relevant API reference section for detailed instructions.

<br />

If you want to practice using the Fire Payments API endpoints listed below, Fire has recipes created in Javascript to see how to use the API to do things like call a list of your accounts. To use these, you'll need our OpenAPI definition document, which you can download from our Github [here.](https://github.com/firefinancialservices/fire-business-api-openapi).  You can use these endpoints to generate reports on your Fire accounts, or to quickly create new accounts as you need them. 

> Please note that amounts are returned in cents (e.g. 100 will equal 1 euro/sterling)

<br />

### Accounts and transactions

<br />

Use our API to edit your accounts and user details. These are accessed and controlled by your account ` ican` or `userId`. To retrieve this number, call the 'Get Details of an Account' first, and use the returned array to pull the information. 

* [Get details of an account](https://docs.fire.com/reference/getaccountbyid)
* [List accounts](https://docs.fire.com/reference/getaccounts)
* [Get account activity](https://docs.fire.com/reference/getactivities)
* [Create a new Fire account](https://docs.fire.com/reference/addaccount)
* [Update account configuration](https://docs.fire.com/reference/updateaccountconfig)
* [List transactions on an account](https://docs.fire.com/reference/gettransactionsbyaccountidv3)

<br />

*See how to write a script to use these endpoints here*

<TutorialTile backgroundColor="#2c4185" emoji="🌐" id="67ed4e2e880bdb0061748c8e" link="https://docs.fire.com/v2.0/recipes/list-accounts-and-balances-1" slug="list-accounts-and-balances-1" title="List Accounts and Balances" />

<br />

### Payees

<br />

Use our API to retrieve payee details on your account. Payee information is retrieved using the  `payeeId` attribute. This can be found first by calling 'List Payee Accounts'.

* [Get details of a payee account](https://docs.fire.com/reference/getpayeeaccountinfo)
* [List transaction to a payee account](https://docs.fire.com/reference/getpayeetransactioninfo)
* [List payee accounts](https://docs.fire.com/reference/getpayees)

<br />

*See how to write a script to use these endpoints here*

<TutorialTile backgroundColor="#2c4185" emoji="🗯️" id="67f6378275eabc0052ced1a6" link="https://docs.fire.com/v2.0/recipes/list-payee-transactions" slug="list-payee-transactions" title="List Payee Transactions" />

<br />

<br />

### Direct debits

<br />

Use our API to set up and manage direct debits on your account. Specific direct debits are identified by '`directDebitUuid'`, which you can find by calling 'List all Direct Debits' first.

* [List all direct debits](https://docs.fire.com/reference/getdirectdebitmandates)
* [Get the details of a direct debit](https://docs.fire.com/reference/getdirectdebitbyuuid)
* [Get the details of a direct debit mandate](https://docs.fire.com/reference/getmandate)
* [List all direct debit mandates](https://docs.fire.com/reference/getdirectdebitmandates)
* [Reject a direct debit](https://docs.fire.com/reference/rejectdirectdebit)
* [Activate a direct debit mandate](https://docs.fire.com/reference/activatemandate)
* [Cancel a direct debit mandate](https://docs.fire.com/reference/cancelmandatebyuuid)
* [Update direct debit mandate alias](https://docs.fire.com/reference/updatemandatealias)

<br />

*See how to write a script to use these endpoints here*

<TutorialTile backgroundColor="#2c4185" emoji="💻" id="67f638fffb12a00010006437" link="https://docs.fire.com/v2.0/recipes/list-all-payments-associated-with-a-direct-debit" slug="list-all-payments-associated-with-a-direct-debit" title="List all payments associated with a Direct Debit" />

<br />

<br />

<br />

### Profile management

<br />

Use our API to get information on your users and account settings.

* [Get the details of a user](https://docs.fire.com/reference/getuser)
* [Get the address of a user](https://docs.fire.com/reference/getuseraddress)
* [List all users](https://docs.fire.com/reference/getusers)
* [List all limits](https://docs.fire.com/reference/getlimits-1)
* [Get service fees and info](https://docs.fire.com/reference/getservicefees)

<br />

<br />

*See how to write a script to use these endpoints here*

<TutorialTile backgroundColor="#2c4185" emoji="🤸‍♂️" id="67f63b534e85c6002a879f03" link="https://docs.fire.com/v2.0/recipes/list-all-users" slug="list-all-users" title="List all users" />

<br />

<br />

***

<br />

Fire customers use our API to streamline and automate payment processes. For example, [Accelerated Payments](https://www.fire.com/case-studies/efficient-reconciliation-and-payouts-across-multiple-accounts/) use the Fire Payments API to instantly open multiple euro and sterling accounts, resulting in a clear and fast flow of payments with real-time transfers and information.
