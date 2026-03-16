# PaymentPaid

Zero-amount Invoice 0 that completed synchronously to PAID


## Fields

| Field                                              | Type                                               | Required                                           | Description                                        |
| -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| `invoice_id`                                       | *str*                                              | :heavy_check_mark:                                 | The Invoice 0 id                                   |
| `amount`                                           | *str*                                              | :heavy_check_mark:                                 | Payment amount ('0' for zero-amount subscriptions) |
| `status`                                           | *Literal["paid"]*                                  | :heavy_check_mark:                                 | Payment status                                     |