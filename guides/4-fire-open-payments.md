---
title: Fire Open Payments
excerpt: Fire Open Payments is a feature of the fire.com business account that leverages Open Banking to allow your customers to pay you via bank transfer and to reconcile those payments as they are received into your fire.com GBP or EUR account.
category: 5f6fc3cc6768a5003ca89038
slug: fire-open-payments
---
To set up each Fire Open Payment you first need to create a payment request. This contains the details of the payment such as the amount, destination account, description as well as various other specific fields that you want to associate with the payment. The payment request is represented as a URL with a unique code which can then be incorporated into an eCommerce shopping cart as an alternative form of payment. For example, you can put "Pay by Bank" on your website along with "Pay by Card" and "Pay by PayPal". It can also be distributed by a variety of means such as by email, SMS, WhatsApp, encoded as a QR code, NFC tag, etc.

Consumers confirm the payment details such as the amount are correct, select their bank and authorise the payment. Payments can be made from all major UK banks.

The funds are settled into your fire.com account, fully reconciled, with your specified fields provided.

There are two implementation options you can use to display payment pages with Fire Open Payments.

1. **Hosted Payment Pages**: fire.com hosts the payment pages - this option allows you to re-direct your customer to the hosted fire.com payment pages displaying the payment details confirmation, bank selection, consent and response pages.
2. **Integrated Payment Pages**: You host the payments page yourself - this option allows you to have control of the UI and UX for displaying the payment details confirmation, bank selection and response pages. Once the response is received, fire.com can re-direct the payer back to your website.

## Hosted Payment Pages Option
    ![Image](https://fire.com/docs/images/fop-hosted-flow.png)

The payer is brought through the following stages to complete the payment:

1. **View Payment Details / Select Account Provider**: The payer must first be clear on the amount of the payment, who they are paying and the reason for the payment. They then select their bank. This step is offered as part of the fire.com payment UI.
1. **Consent page**: The payer must provide consent to the PISP (fire.com) prior to authorising the payment. This is a regulatory requirement, this page must be hosted by fire.com.
1. **Authenticate and Authorise Payment**: The payer will be redirected to their bank's online site or mobile banking app. After authenticating, the details of the payment will be displayed, and the payer will authorise the payment.
1. **Response page**: It is a regulatory requirement that the PISP (fire.com) display the results of the payment and provide the same information that would be provided if the payer had made the payment via their banking application. fire.com must display this page, before optionally redirecting the payer back to your website.
To implement the hosted Fire Open Payments option you need to do the following:

You can create a new Fire Open Payment request either within Firework Online or via the API.

1. Create your new API application with the appropriate permissions required in Firework Online, as outlined in the [Authentication](/docs/authentication) steps. The permissions needed are:
   - "Create a Payment Request"
   - "Get Payment Details"

1. Use the Refresh Token, Client ID and Client Key to create an access token as outlined in the [Authentication](/docs/authentication) steps.

1. On your website, create a "Pay by Bank" button alongside your other available payment methods, such as Cards and PayPal.

1. After the user clicks on "Pay by Bank", you need to create a new Fire Open Payment request via the [Create a Fire Open Payment request](/reference/newpaymentrequest) endpoint. This endpoint returns a unique `code` for the payment request. 

1. Create a URL using the code returned in this format: `https://payments.fire.com/{code}` and redirect your customer to this page.

1. fire.com will host all the pages that the customer needs to review and authorise the payment. We will return the `paymentUUID` of the successful or failed transaction to the `returnUrl` that you supplied when creating the Fire Open Payment request. We can also optionally send a webhook to your website notifying you of the transaction's outcome.

1. Once fire.com responds with the `paymentUUID` and/or the webhook to your website, you need to call the [Get Payment Details](/reference/getpaymentdetails) endpoint to get the details of the transaction. This will let you know whether the transaction was successful or not. You can set up the `Payment Request Payment Authorised` webhook to notify you once the payment is authorised or cancelled.

1. The funds will be received into your GBP or EUR account. Funding will typically be within 6 business hours.


