# ListInvoicesRequest


## Fields

| Field                                                                  | Type                                                                   | Required                                                               | Description                                                            |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `limit`                                                                | *Optional[int]*                                                        | :heavy_minus_sign:                                                     | Maximum number of invoices to return                                   |
| `next_action_at`                                                       | [Optional[models.NextActionAt]](../models/nextactionat.md)             | :heavy_minus_sign:                                                     | Filter for invoices ready for processing (platform only)               |
| `status`                                                               | [Optional[models.ListInvoicesStatus]](../models/listinvoicesstatus.md) | :heavy_minus_sign:                                                     | Filter invoices by status                                              |
| `subscription_id`                                                      | *Optional[str]*                                                        | :heavy_minus_sign:                                                     | Filter invoices by subscription ID                                     |