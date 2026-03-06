# ListFeesRequest


## Fields

| Field                                    | Type                                     | Required                                 | Description                              |
| ---------------------------------------- | ---------------------------------------- | ---------------------------------------- | ---------------------------------------- |
| `limit`                                  | *Optional[int]*                          | :heavy_minus_sign:                       | Number of fees to return.                |
| `merchant_id`                            | *str*                                    | :heavy_check_mark:                       | Filter fees by merchant organization ID. |
| `offset`                                 | *Optional[int]*                          | :heavy_minus_sign:                       | Number of fees to skip.                  |
| `product_id`                             | *Optional[str]*                          | :heavy_minus_sign:                       | Filter fees by product ID.               |