# UpdateCustomerNotificationSettings

Notification preferences for this customer. Only provided fields are updated.


## Fields

| Field                                                     | Type                                                      | Required                                                  | Description                                               |
| --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- | --------------------------------------------------------- |
| `invoice_issued`                                          | *Optional[bool]*                                          | :heavy_minus_sign:                                        | Whether to send invoice issued emails to this customer.   |
| `invoice_paid`                                            | *Optional[bool]*                                          | :heavy_minus_sign:                                        | Whether to send invoice paid emails to this customer.     |
| `renewal_reminder`                                        | *Optional[bool]*                                          | :heavy_minus_sign:                                        | Whether to send renewal reminder emails to this customer. |