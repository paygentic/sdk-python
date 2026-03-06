# OffsetPagination

Offset-based pagination response.


## Fields

| Field                                         | Type                                          | Required                                      | Description                                   |
| --------------------------------------------- | --------------------------------------------- | --------------------------------------------- | --------------------------------------------- |
| `limit`                                       | *Optional[int]*                               | :heavy_minus_sign:                            | Number of items returned in the current page. |
| `offset`                                      | *Optional[int]*                               | :heavy_minus_sign:                            | Number of items skipped.                      |
| `total`                                       | *Optional[int]*                               | :heavy_minus_sign:                            | Total number of items available.              |