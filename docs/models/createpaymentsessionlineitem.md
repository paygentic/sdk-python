# CreatePaymentSessionLineItem


## Fields

| Field                                             | Type                                              | Required                                          | Description                                       |
| ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- | ------------------------------------------------- |
| `description`                                     | *str*                                             | :heavy_check_mark:                                | Line item description.                            |
| `amount`                                          | *str*                                             | :heavy_check_mark:                                | Line item amount in decimal format (e.g. '5.00'). |
| `quantity`                                        | *Optional[int]*                                   | :heavy_minus_sign:                                | Quantity of this line item. Defaults to 1.        |