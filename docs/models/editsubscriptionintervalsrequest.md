# EditSubscriptionIntervalsRequest

An add/edit/remove op set to apply to the subscription's price timeline. At least one operation is required.


## Fields

| Field                                                                                  | Type                                                                                   | Required                                                                               | Description                                                                            |
| -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------- |
| `add`                                                                                  | List[[models.SubscriptionIntervalAddOp](../models/subscriptionintervaladdop.md)]       | :heavy_minus_sign:                                                                     | New override segments to add.                                                          |
| `edit`                                                                                 | List[[models.SubscriptionIntervalEditOp](../models/subscriptionintervaleditop.md)]     | :heavy_minus_sign:                                                                     | Changes to existing intervals.                                                         |
| `remove`                                                                               | List[[models.SubscriptionIntervalRemoveOp](../models/subscriptionintervalremoveop.md)] | :heavy_minus_sign:                                                                     | Intervals to remove outright.                                                          |