# ListOrdersRequest


## Fields

| Field                                                              | Type                                                               | Required                                                           | Description                                                        |
| ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ | ------------------------------------------------------------------ |
| `merchant_id`                                                      | *Optional[str]*                                                    | :heavy_minus_sign:                                                 | Filter by merchant                                                 |
| `customer_id`                                                      | *Optional[str]*                                                    | :heavy_minus_sign:                                                 | Filter by customer                                                 |
| `status`                                                           | [Optional[models.ListOrdersStatus]](../models/listordersstatus.md) | :heavy_minus_sign:                                                 | Filter by status                                                   |
| `type`                                                             | [Optional[models.ListOrdersType]](../models/listorderstype.md)     | :heavy_minus_sign:                                                 | Filter by type                                                     |
| `limit`                                                            | *Optional[int]*                                                    | :heavy_minus_sign:                                                 | N/A                                                                |
| `offset`                                                           | *Optional[int]*                                                    | :heavy_minus_sign:                                                 | N/A                                                                |