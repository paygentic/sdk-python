# WebhookPortal


## Fields

| Field                                                                | Type                                                                 | Required                                                             | Description                                                          |
| -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- | -------------------------------------------------------------------- |
| `object`                                                             | [models.WebhookPortalObject](../models/webhookportalobject.md)       | :heavy_check_mark:                                                   | Object type identifier                                               |
| `expires_at`                                                         | [date](https://docs.python.org/3/library/datetime.html#date-objects) | :heavy_check_mark:                                                   | When the portal link expires                                         |
| `url`                                                                | *str*                                                                | :heavy_check_mark:                                                   | Magic link URL to access the webhook portal                          |