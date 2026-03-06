# BulkApproveSourceEventsResponse

Bulk approval results


## Fields

| Field                                                                                          | Type                                                                                           | Required                                                                                       | Description                                                                                    |
| ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------- |
| `processed`                                                                                    | *Optional[int]*                                                                                | :heavy_minus_sign:                                                                             | Number of successfully approved events                                                         |
| `failed`                                                                                       | *Optional[int]*                                                                                | :heavy_minus_sign:                                                                             | Number of events that failed to process                                                        |
| `details`                                                                                      | [Optional[models.BulkApproveSourceEventsDetails]](../models/bulkapprovesourceeventsdetails.md) | :heavy_minus_sign:                                                                             | N/A                                                                                            |