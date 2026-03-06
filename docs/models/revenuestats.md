# RevenueStats


## Fields

| Field                                           | Type                                            | Required                                        | Description                                     |
| ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- | ----------------------------------------------- |
| `usage_revenue`                                 | *Optional[str]*                                 | :heavy_minus_sign:                              | Revenue from usage charges in dollars           |
| `fee_revenue`                                   | *Optional[str]*                                 | :heavy_minus_sign:                              | Revenue from fee charges in dollars             |
| `refund_amount`                                 | *Optional[str]*                                 | :heavy_minus_sign:                              | Total refund amount in dollars                  |
| `net_revenue`                                   | *Optional[str]*                                 | :heavy_minus_sign:                              | Net revenue in dollars (usage + fees - refunds) |
| `usage_count`                                   | *Optional[int]*                                 | :heavy_minus_sign:                              | Number of usage charge events                   |
| `fee_count`                                     | *Optional[int]*                                 | :heavy_minus_sign:                              | Number of fee charge events                     |
| `usage_refund_count`                            | *Optional[int]*                                 | :heavy_minus_sign:                              | Number of usage refund events                   |
| `fee_refund_count`                              | *Optional[int]*                                 | :heavy_minus_sign:                              | Number of fee refund events                     |