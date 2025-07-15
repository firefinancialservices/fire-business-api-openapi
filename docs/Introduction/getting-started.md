---
title: Overview
excerpt: >-
  Fire provides access to a range of payment services, including accounts, bank
  transfers, debit cards, FX, and open banking payments. With our platform and
  licences, we deliver solutions that automate payment processing and make
  reconciliation easier, more cost-effective and secure. The Fire Payments API
  enables you to deeply integrate Business Account features into your
  application or back-office systems. Whether initiating payments out,
  segregating funds or automating reconciliation, our powerful API can be used
  to enhance and simplify a range of payment processes.
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---
## Fire Payments API

Whether initiating payments out, segregating funds or enhancing reconciliation, the Fire Payments API can be used to automate and simplify a range of payment processes. In order to create a Fire account, please contact our [sales](https://www.fire.com/contact-us/) team.

<br />

[block:html]
{
  "html": "<div style=\"display: flex;\">\n  <div style=\"flex: 1; height: 280px; align-items: center; justify-content: center;\">\n    <div><img src=\"https://siteapi.fire.com/wp-content/uploads/2024/06/payments-use-case-1.png\" width=\"260\"></div>\n    <div style=\"padding: 12px 32px\"><a href=\"https://docs.fire.com/docs/payments-accounts#accounts-and-transactions\" style=\"color: #2C4185; text-decoration: none; font-weight: bold;\">Automate Payments Out</a></div>\n    <div style=\"padding: 0px 32px; width: 250px;\">Transfer funds into your Fire account for automatic distribution to employees or contractors.</div>\n  </div>\n\n  <div style=\"flex: 1; height: 280px; align-items: center; justify-content: center;\">\n    <div><img src=\"https://siteapi.fire.com/wp-content/uploads/2024/08/open-banking-use-case-1.png\" width=\"260\"></div>\n    <div style=\"padding: 12px 32px\"><a href=\"https://docs.fire.com/docs/open-banking-payments#how-does-the-fire-payments--api-work-with-open-banking-payments\" style=\"color: #2C4185; text-decoration: none; font-weight: bold;\">Open Banking Payments</a></div>\n    <div style=\"padding: 0px 32px; width: 250px;\">Get paid faster, lower your fees and reduce fraud via account to account payments.</div>\n  </div>\n\n  <div style=\"flex: 1; height: 280px; align-items: center; justify-content: center;\">\n    <div><img src=\"https://siteapi.fire.com/wp-content/uploads/2024/06/payments-use-case-2.png\" width=\"260\"></div>\n    <div style=\"padding: 12px 32px\"><a href=\"https://docs.fire.com/docs/accounts-1#how-can-you-use-fire-to-submit-batch-payments\" style=\"color: #2C4185; text-decoration: none; font-weight: bold;\">Manage Cash Flows</a></div>\n    <div style=\"padding: 0px 32px; width: 250px;\">Initiate large volume batch payments to suppliers or partners through the Fire Payments API.</div>\n  </div>\n</div>"
}
[/block]


***

<br />

## Getting set up

> 📘 With Fire, our API allows different software applications to communicate with our systems. One app sends a request to our API, which the API then retrieves the information or performs an action from another app, then sends the response back.

Firstly, you will need to set up a 'Fire Application' to access the Fire Payments API. This enables you to set up access to your Fire account with the specific permissions you want your application to have. To do this:

1. Login at <https://business.fire.com>.
2. Select the “Settings“ Menu.
3. Select the “API” tab.
4. Click “Add New Application“

![](https://files.readme.io/8c96df64edd7f64951575c0d5644d6e61fdd0e2d3e284ad553703fab43b195f3-image.png)

<br />

5. Give your API Application a name, and select the required permissions. 

![](https://files.readme.io/0fc16a92211aaf2c2dbfe213bd8936927e991fe579ed7f040936e586ebbe29e0-image.png)

<br />

6. Once you have completed the above step, click "Create" and take note of the Client ID, Client Key and Refresh Token - ensure you have noted the Client Key safely as this will not be displayed again.

> _If you ever accidentally reveal the Client Key (or accidentally commit it to Github for instance) it is vital that you log into the Fire desktop application online and delete/recreate the 'App Tokens' as soon as possible. Anyone who has these three pieces of data can access the API to view your data and set up payments from your account (depending on the scope of the tokens)._

<br />

<br />

***

## Using the Fire Payments API

These guides will explain how the Fire Payments API works in relation to our product offering, and our references will help you integrate it in to your back-end. 

Fire customers use our API to create customised applications to solve specific problems. For example [Goodbox](https://www.fire.com/case-studies/automating-payouts-to-partners-through-full-api-integration/)  automated their payments to partners through full API integration