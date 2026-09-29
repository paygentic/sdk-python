# CreateItemRequest


## Fields

| Field                                 | Type                                  | Required                              | Description                           |
| ------------------------------------- | ------------------------------------- | ------------------------------------- | ------------------------------------- |
| `merchant_id`                         | *str*                                 | :heavy_check_mark:                    | Unique identifier for an organization |
| `name`                                | *str*                                 | :heavy_check_mark:                    | Canonical sellable name for the Item  |
| `catalog_id`                          | *Optional[str]*                       | :heavy_minus_sign:                    | Unique identifier for a product       |
| `metadata`                            | Dict[str, *Any*]                      | :heavy_minus_sign:                    | Optional key-value metadata           |