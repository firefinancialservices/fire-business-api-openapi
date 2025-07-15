---
title: Add a bank transfer to a batch.
excerpt: >-
  This endpoint will add a new bank transfer payment to a batch. There are two
  ways to process bank transfers - by Payee ID (**Mode 1**) or by Payee Account
  Details (**Mode 2**).


  **Mode 1:** Use the payee IDs of existing approved payees set up against your
  account. These batches can be approved in the normal manner.


  **Mode 2:** Use the account details of the payee. In the event that these
  details correspond to an existing approved payee, the batch can be approved as
  normal. If the account details are new, a batch of New Payees will
  automatically be created. This batch will need to be approved before the
  Payment batch can be approved. These payees will then exist as approved payees
  for future batches.

  You will need to enable PERM_BUSINESS_POST_BATCH_BANKTRANSFERS to use this
  endpoint.
api:
  file: fire-financial-services-business-api.json
  operationId: addBankTransferBatchPayment
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---