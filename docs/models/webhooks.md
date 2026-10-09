# Webhooks


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `object`                                                             | [models.WebhooksObject](../models/webhooksobject.md)                 | :heavy_check_mark:                                                   | Object type identifier                                               |
| `application_id`                                                     | *str*                                                                | :heavy_check_mark:                                                   | Svix application identifier                                          |
| `created_at`                                                         | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | When webhooks were first enabled                                     |
| `enabled`                                                            | *bool*                                                               | :heavy_check_mark:                                                   | Whether webhooks are enabled                                         |
| `merchant_id`                                                        | *str*                                                                | :heavy_check_mark:                                                   | Merchant identifier                                                  |
| `updated_at`                                                         | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | When webhooks were last updated                                      |