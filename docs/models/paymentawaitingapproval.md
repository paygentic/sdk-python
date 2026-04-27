# PaymentAwaitingApproval

Invoice 0 awaiting merchant approval before payment can proceed. The invoice is in DRAFT status with totals calculated. Approval is a platform-managed action and will be available via a public endpoint in a future release.


## Fields

| Field                                         | Type                                          | Required                                      | Description                                   |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| `invoice_id`                                  | *str*                                         | :heavy_check_mark:                            | The Invoice 0 id awaiting approval            |
| `amount`                                      | *str*                                         | :heavy_check_mark:                            | Total payment amount in decimal dollar format |
| `status`                                      | *Literal["awaiting_approval"]*                | :heavy_check_mark:                            | Payment status                                |