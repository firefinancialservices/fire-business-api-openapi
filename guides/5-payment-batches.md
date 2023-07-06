---
title: Payment Batches
excerpt: The fire.com API allows businesses to automate payments between their accounts or to third parties across the UK and Europe.
category: 5f6fc3cc6768a5003ca89038
slug: batch-payments
---
For added security, the API can only set up the payments in batches. These batches must be approved by an authorised user via the firework mobile app.


The process is as follows:


**1.**Create a new batch
**2.**Add payments to the batch
**3.**Submit the batch for approval


Once the batch is submitted, the authorised users will receive notifications to their firework mobile apps. They can review the contents of the batch and then approve or reject it. If approved, the batch is then processed. You can avail of enhanced security by using Dual Authorisation to verify payments if you wish. Dual Authorisation can be enabled by you when setting up your API application in firework online.


**Batch Life Cycle Events**


A batch webhook can be specified to receive details of all the payments as they are processed. This webhook receives notifications for every event in the batch lifecycle.


The following events are triggered during a batch:


**batch.opened:** Contains the details of the batch opened. Checks that the callback URL exists - unless a HTTP 200 response is returned, the callback URL will not be configured.


**batch.item-added:** Details of the item added to the batch


**batch.item-removed:** Details of the item removed from the batch


**batch.cancelled:** Notifies that the batch was cancelled.


**batch.submitted:** Notifes that the batch was submitted


**batch.approved:** Notifies that the batch was approved.


**batch.rejected:** Notifies that the batch was rejected.


**batch.failed:** Notifies that the batch failed - includes the details of the failure (insufficient funds etc)


**batch.completed:** Notifies that the batch completed successfully. Includes a summary.


Push notifications are sent to the firework mobile app for many of these events too - these can be configured from within the app.


This is the first step in creating a batch payment.

