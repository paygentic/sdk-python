# GetInvoiceRequest


## Fields

| Field                                                                   | Type                                                                    | Required                                                                | Description                                                             |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------------- |
| `id`                                                                    | *str*                                                                   | :heavy_check_mark:                                                      | The invoice ID                                                          |
| `expand`                                                                | *Optional[str]*                                                         | :heavy_minus_sign:                                                      | Comma-separated list of fields to expand. Currently supports: lineItems |
| `line_items_limit`                                                      | *Optional[int]*                                                         | :heavy_minus_sign:                                                      | Page size for line items when expand=lineItems                          |
| `line_items_page_token`                                                 | *Optional[str]*                                                         | :heavy_minus_sign:                                                      | Pagination token for line items when expand=lineItems                   |