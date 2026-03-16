# PaymentSummary


## Fields

| Field                                              | Type                                               | Required                                           | Description                                        |
| -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| `completed_count`                                  | *int*                                              | :heavy_check_mark:                                 | Number of completed payment links in the period    |
| `completed_amount`                                 | *str*                                              | :heavy_check_mark:                                 | Total amount of completed payment links in dollars |
| `pending_count`                                    | *int*                                              | :heavy_check_mark:                                 | Number of pending payment links in the period      |
| `pending_amount`                                   | *str*                                              | :heavy_check_mark:                                 | Total amount of pending payment links in dollars   |
| `expired_count`                                    | *int*                                              | :heavy_check_mark:                                 | Number of expired payment links in the period      |
| `expired_amount`                                   | *str*                                              | :heavy_check_mark:                                 | Total amount of expired payment links in dollars   |