# LineItemsResponse


## Fields

| Field                                                                  | Type                                                                   | Required                                                               | Description                                                            |
| ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- | ---------------------------------------------------------------------- |
| `object`                                                               | [models.LineItemsResponseObject](../models/lineitemsresponseobject.md) | :heavy_check_mark:                                                     | The object type                                                        |
| `data`                                                                 | List[[models.LineItem](../models/lineitem.md)]                         | :heavy_check_mark:                                                     | Array of line items                                                    |
| `total_count`                                                          | *int*                                                                  | :heavy_check_mark:                                                     | Total number of matching line items                                    |
| `summary`                                                              | [models.LineItemsSummary](../models/lineitemssummary.md)               | :heavy_check_mark:                                                     | N/A                                                                    |