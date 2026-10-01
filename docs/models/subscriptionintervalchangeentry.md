# SubscriptionIntervalChangeEntry

One interval that the change added, edited or removed, with its state before and after.


## Fields

| Field                                                                                          | Type                                                                                           | Required                                                                                       | Description                                                                                    |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `interval_id`                                                                                  | *str*                                                                                          | :heavy_check_mark:                                                                             | N/A                                                                                            |
| `before`                                                                                       | [Nullable[models.SubscriptionIntervalChangeCopy]](../models/subscriptionintervalchangecopy.md) | :heavy_check_mark:                                                                             | The interval before the edit. Null when the edit added it.                                     |
| `after`                                                                                        | [Nullable[models.SubscriptionIntervalChangeCopy]](../models/subscriptionintervalchangecopy.md) | :heavy_check_mark:                                                                             | The interval after the edit. Null when the edit removed it.                                    |