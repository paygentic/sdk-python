# ListBillingSchedulesRequest


## Fields

| Field                                            | Type                                             | Required                                         | Description                                      |
| ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ | ------------------------------------------------ |
| `order_id`                                       | *Optional[str]*                                  | :heavy_minus_sign:                               | Filter by owning order (XOR with subscriptionId) |
| `subscription_id`                                | *Optional[str]*                                  | :heavy_minus_sign:                               | Filter by owning subscription (XOR with orderId) |