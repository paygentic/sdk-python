# SubscriptionCustomer

Customer details with merchant and consumer information. Only included when include=customer is specified in the list query.


## Fields

| Field                                              | Type                                               | Required                                           | Description                                        |
| -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| `id`                                               | *Optional[str]*                                    | :heavy_minus_sign:                                 | Customer ID                                        |
| `merchant_id`                                      | *Optional[str]*                                    | :heavy_minus_sign:                                 | Merchant organization ID                           |
| `merchant`                                         | [Optional[models.Merchant]](../models/merchant.md) | :heavy_minus_sign:                                 | N/A                                                |
| `consumer`                                         | [Optional[models.Consumer]](../models/consumer.md) | :heavy_minus_sign:                                 | N/A                                                |