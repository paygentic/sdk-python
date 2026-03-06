# ListBillableMetricsRequest


## Fields

| Field                                                | Type                                                 | Required                                             | Description                                          |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| `limit`                                              | *Optional[int]*                                      | :heavy_minus_sign:                                   | Number of billable metrics to return.                |
| `merchant_id`                                        | *str*                                                | :heavy_check_mark:                                   | Filter billable metrics by merchant organization ID. |
| `offset`                                             | *Optional[int]*                                      | :heavy_minus_sign:                                   | Number of billable metrics to skip.                  |
| `product_id`                                         | *Optional[str]*                                      | :heavy_minus_sign:                                   | Filter billable metrics by product ID.               |