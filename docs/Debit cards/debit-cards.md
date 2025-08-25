---
title: Get started with debit cards
metadata:
  title: ''
  description: ''
  robots: index
content:
  excerpt: >-
    Manage your business expenses and subscriptions.


    Fire is a principal issuer of MasterCard® since 2016, making us one of the
    first payment institutions to be authorised as a member. Our debit cards can
    be used for in-store payments, online shopping, and ATM cash withdrawals. We
    employ security protocols such as Strong Customer Authentication (SCA) and
    3D Secure (3DS) to bolster the safety of our debit cards. We ensure that our
    customers' transactions are protected against unauthorised access,
    reinforcing our commitment to providing a trusted and secure financial
    experience.
privacy:
  view: public
---
## Why choose Fire's debit cards?

<br />

<HTMLBlock>{`
<div style="display: flex;">
  <div style="flex: 1; height: 280px; align-items: center; justify-content: center;">
    <div><img src="https://www.fire.com/_next/image/?url=https%3A%2F%2Fsiteapi.fire.com%2Fwp-content%2Fuploads%2F2024%2F06%2FDebit-use-case-2.png&w=1920&q=75" width="350"></div>
    <div style="padding: 12px 32px"><a href="https://docs.fire.com/docs/debit-cards#what-can-you-do-with-your-fire-debit-card" style="color: #2C4185; text-decoration: none; font-weight: bold;">Manage your cards</a></div>
    <div style="padding: 0px 32px; width: 350px;">Issue Fire debit cards for each of your accounts ensuring a controlled and fully reconcilable card spending environment.</div>
  </div>

  <div style="flex: 1; height: 280px; align-items: center; justify-content: center;">
    <div><img src="https://www.fire.com/_next/image/?url=https%3A%2F%2Fsiteapi.fire.com%2Fwp-content%2Fuploads%2F2024%2F08%2Fopen-banking-use-case-1.png&w=1920&q=75" width="350"></div>
    <div style="padding: 12px 32px"><a href="https://docs.fire.com/docs/open-banking-payments#how-does-the-fire-payments--api-work-with-open-banking-payments" style="color: #2C4185; text-decoration: none; font-weight: bold;">Real-time webhooks</a></div>
    <div style="padding: 0px 32px; width: 350px;">Get instant payment notifications for every authorisation so you can remain in control.</div>
  </div>
`}</HTMLBlock>

<br />

Find more use cases and examples on [Fire's website](https://www.fire.com/services/debit-cards/).

***

## What can you do with your Fire debit card?

> 📘 See the Debit Cards reference section for more detailed instructions

<br />

If you want to practice using the Fire Payments API endpoints listed below, Fire has recipes created in Javascript to see how to use the API to do things like see a list of the cards on your account. To use these, you'll need our OpenAPI definition document, which you can download from our Github [here.](https://github.com/firefinancialservices/fire-business-api-openapi). You can use these endpoints to view the cards associated with your accounts, control your cards and view transactions. 

* [List debit cards](https://docs.fire.com/reference/getlistofcards)
* [Get a list of debit card transactions](https://docs.fire.com/reference/getlistofcardtransactions)
* [Create a new Fire debit card](https://docs.fire.com/reference/createnewcard)
* [Block a Fire debit card](https://docs.fire.com/reference/blockcard)
* [Unblock a Fire debit card](https://docs.fire.com/reference/unblockcard)

<br />

*See how to write a script to use these endpoints here*

<TutorialTile backgroundColor="#2c4185" emoji="💳" id="67f660d8947ad2000fe8d84c" link="https://docs.fire.com/v2.0/recipes/list-the-cards-on-your-account" slug="list-the-cards-on-your-account" title="List the cards on your account" />

<br />

***

<br />

Fire customers can leverage our API to control multiple business debit cards and accounts. For example,[ the Joe Duffy Group](https://www.fire.com/case-studies/leveraging-multiple-debit-cards-to-manage-expenses/) manages its expenses and budgets using multiple debit cards.
