# GroupInvoiceSummary


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `group_key`                                                          | *str*                                                                | :heavy_check_mark:                                                   | Unique identifier for the group (e.g. plan ID, or 'other')           |
| `group_label`                                                        | *str*                                                                | :heavy_check_mark:                                                   | Human-readable label for the group (e.g. plan name)                  |
| `outstanding`                                                        | [models.InvoiceCategorySummary](../models/invoicecategorysummary.md) | :heavy_check_mark:                                                   | N/A                                                                  |
| `paid`                                                               | [models.InvoiceCategorySummary](../models/invoicecategorysummary.md) | :heavy_check_mark:                                                   | N/A                                                                  |
| `written_off`                                                        | [models.InvoiceCategorySummary](../models/invoicecategorysummary.md) | :heavy_check_mark:                                                   | N/A                                                                  |