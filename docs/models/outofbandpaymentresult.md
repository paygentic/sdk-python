# OutOfBandPaymentResult


## Fields

| Field                                               | Type                                                | Required                                            | Description                                         |
| --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- | --------------------------------------------------- |
| `method`                                            | *Literal["out_of_band"]*                            | :heavy_check_mark:                                  | Discriminator: an out-of-band payment was recorded. |
| `invoice`                                           | [models.Invoice](../models/invoice.md)              | :heavy_check_mark:                                  | N/A                                                 |