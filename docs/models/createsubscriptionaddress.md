# CreateSubscriptionAddress

Address is required for tax calculation. Must include: country (ISO 3166-1 alpha-2) and zipCode. The state/region field is required and validated for US/CA addresses only (custom validation in API logic). Postal code format is not validated but will be normalized.


## Fields

| Field                             | Type                              | Required                          | Description                       |
| --------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- |
| `line1`                           | *Optional[str]*                   | :heavy_minus_sign:                | N/A                               |
| `line2`                           | *Optional[str]*                   | :heavy_minus_sign:                | N/A                               |
| `city`                            | *Optional[str]*                   | :heavy_minus_sign:                | N/A                               |
| `state`                           | *Optional[str]*                   | :heavy_minus_sign:                | N/A                               |
| `country`                         | *str*                             | :heavy_check_mark:                | 2 character ISO 3166 country code |
| `zip_code`                        | *str*                             | :heavy_check_mark:                | N/A                               |