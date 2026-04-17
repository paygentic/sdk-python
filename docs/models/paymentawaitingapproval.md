# PaymentAwaitingApproval

Invoice 0 awaiting merchant approval before payment can proceed. The invoice is in DRAFT status with totals calculated. Approval is currently platform-only — do not call PATCH /v2/invoices/{id} with {"trigger": "APPROVE"} from merchant credentials (it will return 403). A merchant-accessible approval endpoint is planned for PAYG-754.


## Fields

| Field                                         | Type                                          | Required                                      | Description                                   |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| `invoice_id`                                  | *str*                                         | :heavy_check_mark:                            | The Invoice 0 id awaiting approval            |
| `amount`                                      | *str*                                         | :heavy_check_mark:                            | Total payment amount in decimal dollar format |
| `status`                                      | *Literal["awaiting_approval"]*                | :heavy_check_mark:                            | Payment status                                |