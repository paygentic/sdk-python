# BulkApproveSourceEventsDetails


## Fields

| Field                                                                                    | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `processed`                                                                              | List[*str*]                                                                              | :heavy_minus_sign:                                                                       | IDs of successfully processed events                                                     |
| `failed`                                                                                 | List[[models.BulkApproveSourceEventsFailed](../models/bulkapprovesourceeventsfailed.md)] | :heavy_minus_sign:                                                                       | Failed events with error messages                                                        |