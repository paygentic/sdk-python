# FeePrice

The price configuration for a fee within a subscription context.


## Fields

| Field                                                          | Type                                                           | Required                                                       | Description                                                    |
| -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| `id`                                                           | *str*                                                          | :heavy_check_mark:                                             | The unique identifier of the price.                            |
| `fee_id`                                                       | *str*                                                          | :heavy_check_mark:                                             | The unique identifier of the fee.                              |
| `model`                                                        | [models.FeePriceModel](../models/feepricemodel.md)             | :heavy_check_mark:                                             | The pricing model. Fees only support standard pricing.         |
| `payment_term`                                                 | [models.FeePricePaymentTerm](../models/feepricepaymentterm.md) | :heavy_check_mark:                                             | When the fee is charged relative to the billing period.        |
| `invoice_display_name`                                         | *str*                                                          | :heavy_check_mark:                                             | The name to display on invoices for this fee.                  |
| `properties`                                                   | [models.Properties](../models/properties.md)                   | :heavy_check_mark:                                             | N/A                                                            |
| `tax_rate`                                                     | *Optional[float]*                                              | :heavy_minus_sign:                                             | The tax rate as a percentage (e.g., 10 for 10%).               |