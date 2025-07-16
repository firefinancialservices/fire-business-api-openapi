---
title: Submit a batch
excerpt: >
  This endpoint allows you to submit a Batch (for approval in the case of a
  **BANK_TRANSFER** or **INTERNATIONAL_TRANSFER**). If this is an
  **INTERNAL_TRANSFER** batch, the transfers are immediately queued for
  processing. If this is a **BANK_TRANSFER** or **INTERNATIONAL_TRANSFER**
  batch, this will trigger requests for approval to the firework mobile apps of
  authorised users. Once those users approve the batch, it is queued for
  processing.


  You can only submit a batch while it is in the OPEN state. You will need to
  enable PERM_BUSINESS_PUT_BATCH to use this endpoint.
api:
  file: .fire-business-api-v1.yaml
  operationId: submitBatch
hidden: false
---