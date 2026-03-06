# InvoiceLineItemsResponse


## Fields

| Field                                                        | Type                                                         | Required                                                     | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `invoice_id`                                                 | *str*                                                        | :heavy_check_mark:                                           | The invoice ID                                               |
| `line_items`                                                 | List[[models.InvoiceLineItem](../models/invoicelineitem.md)] | :heavy_check_mark:                                           | Array of line items for this page                            |
| `next_page_token`                                            | *OptionalNullable[str]*                                      | :heavy_minus_sign:                                           | Token for fetching the next page, null if no more pages      |
| `total_count`                                                | *int*                                                        | :heavy_check_mark:                                           | Total number of line items across all pages                  |