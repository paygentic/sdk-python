# OffsetPagination

Offset-based pagination response.


## Fields

| Field                            | Type                             | Required                         | Description                      |
| -------------------------------- | -------------------------------- | -------------------------------- | -------------------------------- |
| `limit`                          | *int*                            | :heavy_check_mark:               | Requested page size.             |
| `offset`                         | *int*                            | :heavy_check_mark:               | Number of items skipped.         |
| `total`                          | *int*                            | :heavy_check_mark:               | Total number of items available. |