---
title: Get started with open banking
excerpt: >-
  Get paid faster, lower your fees and reduce fraud. Fire is among the first
  companies in Ireland and the UK to offer open banking payment acceptance,
  viewing it as the initial stage of account-based payments. We anticipate
  further innovation and regulatory changes leading to the evolution of
  account-based payments beyond open banking. As a dually regulated business,
  Fire uses its own technology and licences to provide payment services and is
  dedicated to introducing this new payment method to the Irish and UK markets.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
> 📘 *Open Banking account-to-account (A2A) payments refer to a payment method where funds are transferred directly between bank accounts via an open banking platform. This method leverages APIs to allow third-party providers (TPPs) to access and initiate payments directly from a payer's bank account to a recipient's account, without the need for traditional card networks or intermediaries.*
>
> With Fire, you can enhance your payment acceptance process by enabling your customers to pay directly from their accounts. During the payment process, customers are redirected to their banking apps where they instantly approve the payment.

***

<br />

## Why choose Fire open banking payments?

*We developed our open banking payment acceptance solution with a holistic and merchant-focused approach, providing a full service to merchants – from payment initiation to collections, reconciliation, settlement, and refunds.*

<br />

To set up each Fire Open Payment you first need to create a payment request. This contains the details of the payment such as the amount, destination account, description as well as various other specific fields that you want to associate with the payment. The payment request is represented as a URL with a unique code which can then be incorporated into an eCommerce shopping cart as an alternative form of payment. For example, you can put "Pay by Bank" on your website along with "Pay by Card" and "Pay by PayPal". It can also be distributed by a variety of means such as by email, SMS, WhatsApp, encoded as a QR code, NFC tag, etc.

Consumers confirm the payment details such as the amount are correct, select their bank and authorise the payment. Payments can be made from all major UK banks.

<HTMLBlock>{`
<div style="display: flex;">
  <div style="flex: 1; height: 280px; align-items: center; justify-content: center;">
    <div><img src="https://www.fire.com/_next/image/?url=https%3A%2F%2Fsiteapi.fire.com%2Fwp-content%2Fuploads%2F2024%2F06%2Fopen-banking-use-case-2.png&w=1920&q=75" width="350"></div>
    <div style="padding: 12px 32px"><a href="https://docs.fire.com/docs/open-banking-payments#how-does-the-fire-payments--api-work-with-open-banking-payments" style="color: #2C4185; text-decoration: none; font-weight: bold;">Customised screens</a></div>
    <div style="padding: 0px 32px; width: 350px;">Apply your own logic to manage and split funds. Initiate payouts via the Fire Payments API.</div>
  </div>

  <div style="flex: 1; height: 280px; align-items: center; justify-content: center;">
    <div><img src="https://www.fire.com/_next/image/?url=https%3A%2F%2Fsiteapi.fire.com%2Fwp-content%2Fuploads%2F2024%2F08%2Fopen-banking-use-case-1.png&w=1920&q=75" width="350"></div>
    <div style="padding: 12px 32px"><a href="https://docs.fire.com/docs/open-banking-payments#how-does-the-fire-payments--api-work-with-open-banking-payments" style="color: #2C4185; text-decoration: none; font-weight: bold;">Account-to-account payments</a></div>
    <div style="padding: 0px 32px; width: 350px;">Enhance your payment acceptance process by enabling your customers to pay directly from their accounts. Customers are redirected to their banking apps where they instantly approve the payment.</div>
  </div>
`}</HTMLBlock>

<br />

Fire's solution helps you to manage all your payment needs - payment acceptance, automating payouts, segregating funds, segregating fees and expense management.

<br />

Find more use cases and try making an open banking payment on [Fire's website](https://www.fire.com/services/open-banking-payments/).

***

## Payment requests and implementation

There are two implementation options you can use with Fire to make use of open banking payments. Firstly, to set up each payment, you first need to create a *payment request*. This contains the details of the payment such as the amount, destination account, description as well as various other specific fields that you want to associate with the payment. The payment request is represented as a URL with a unique code which can then be incorporated into an eCommerce shopping cart as an alternative form of payment. For example, you can place a "Pay by Bank" option on your website along with "Pay by Card" and "Pay by PayPal". It can also be distributed by a variety of means such as by email, SMS, WhatsApp, encoded as a QR code, NFC tag, etc.

Consumers can then select their bank and authorise the payment.

The funds are settled into your Fire account, fully reconciled, with your specified fields provided.

![](https://files.readme.io/590d6e8c3c78a33af984c3d6f7fa47fa96eb43a3d2502ce61fd71cf60b675e9b-image.png)

<br />

There are then two implementation options you can use to display payment pages with Fire Open Banking Payments.

* **Hosted payment pages:**
  * Fire hosts the payment pages - this option allows you to re-direct your customer to the hosted Fire payment pages displaying the payment details confirmation, bank selection, consent and response pages.
* **Integrated payment pages:** 
  * You host the payments page yourself - this option allows you to have control of the UX and UI for displaying the payment details confirmation, bank selection and response pages. Once the response is received, Fire can re-direct the payer back to your website.

***

<br />

## How does the Fire Payments  API work with open banking payments?

> 📘 See the Open banking payments reference section for more detailed information.

If you want to practice using the Fire Payments API endpoints listed below, Fire has recipes created in Javascript to see how to use the API to do things like creating a payment request. To use these, you'll need our OpenAPI definition document, which you can download from our Github [here.](https://github.com/firefinancialservices/fire-business-api-openapi). The Fire API can be used to facilitate, but also complement, your open banking product. You can use the API to [create payment requests](https://docs.fire.com/reference/newpaymentrequest) (create the open banking payment link), but also to check [what banks](https://docs.fire.com/reference/getlistofaspsps) are available to pay from, and see [previous transactions](https://docs.fire.com/reference/getpaymentrequestssentv2). 

* [Create a payment request](https://docs.fire.com/reference/newpaymentrequest)
* [Get list of ASPSPs/banks](https://docs.fire.com/reference/getlistofaspsps)
* [Get payment details](https://docs.fire.com/reference/getpaymentdetailsv2)
* [Get list of all payment attempts related to a payment request](https://docs.fire.com/reference/getpaymentrequestpaymentsv2)
* [Get list of all payment requests sent and their details](https://docs.fire.com/reference/getpaymentrequestssentv2)
* [Get a report from a payment request](https://docs.fire.com/reference/getpaymentrequestreportv2)
* [Get a list of payment request transactions](https://docs.fire.com/reference/getpaymentrequestssentv2)
* [Get a public payment request](https://docs.fire.com/reference/getpublicpaymentrequest)
* [Update the status of a payment request](https://docs.fire.com/reference/updatepaymentrequest)

<br />

<br />

*See how to write a script to use these endpoints here*

<TutorialTile backgroundColor="#2c4185" emoji="🤝" id="67f6521000aa510055fe1ccd" link="https://docs.fire.com/v2.0/recipes/create-a-payment-request" slug="create-a-payment-request" title="Create a payment request" />

<br />

***

<br />

Read how the [Irish Guide Dogs for the Blind]() used open banking payments to bring fundraising into the digital era.
