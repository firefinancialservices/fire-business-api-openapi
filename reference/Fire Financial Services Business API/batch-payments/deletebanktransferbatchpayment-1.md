---
title: Remove a bank transfer from a batch.
excerpt: >-
  This endpoint will remove a payment from the Batch (Bank Transfers). You can
  only remove payments before the batch is submitted for approval (while it is
  in the OPEN state). You will need to enable
  PERM_BUSINESS_DELETE_BATCH_BANKTRANSFERS to use this endpoint.
api:
  file: .fire-business-api-v1.yaml
  operationId: deleteBankTransferBatchPayment
hidden: false
---