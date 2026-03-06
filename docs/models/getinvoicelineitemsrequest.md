# GetInvoiceLineItemsRequest


## Fields

| Field                                                  | Type                                                   | Required                                               | Description                                            |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| `id`                                                   | *str*                                                  | :heavy_check_mark:                                     | The invoice ID                                         |
| `limit`                                                | *Optional[int]*                                        | :heavy_minus_sign:                                     | Maximum number of line items to return                 |
| `page_token`                                           | *Optional[str]*                                        | :heavy_minus_sign:                                     | Token for pagination to fetch the next page of results |