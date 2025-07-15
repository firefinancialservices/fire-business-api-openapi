---
title: Activate a direct debit mandate
excerpt: >-
  This endpoint can only be used to activate a direct debit mandate when it is
  in the status REJECT_REQUESTED (even if the account has direct debits
  disabled). This action will also enable the account for direct debits if it
  was previously set to be disabled. You will need to enable
  PERM_BUSINESS_POST_MANDATE_ACTIVATE to use this endpoint.
api:
  file: fire-financial-services-business-api.json
  operationId: activateMandate
deprecated: false
hidden: false
metadata:
  title: ''
  description: ''
  robots: index
next:
  description: ''
---