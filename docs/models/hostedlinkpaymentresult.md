# HostedLinkPaymentResult


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `method`                                                             | *Literal["hosted_link"]*                                             | :heavy_check_mark:                                                   | Discriminator: a hosted payment link was minted/regenerated.         |
| `provider`                                                           | [models.InvoicePaymentProvider](../models/invoicepaymentprovider.md) | :heavy_check_mark:                                                   | The payment provider that a hosted payment link routes to.           |
| `payment_session_id`                                                 | *str*                                                                | :heavy_check_mark:                                                   | The newly created payment session ID.                                |
| `payment_url`                                                        | *str*                                                                | :heavy_check_mark:                                                   | The customer-facing payment link for the new session.                |
| `invoice`                                                            | [models.Invoice](../models/invoice.md)                               | :heavy_check_mark:                                                   | N/A                                                                  |