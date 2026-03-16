# ListEntitlementGrantsResponse

Successfully retrieved the list of grants.


## Fields

| Field                                                                                    | Type                                                                                     | Required                                                                                 | Description                                                                              |
| ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------- |
| `object`                                                                                 | [Optional[models.ListEntitlementGrantsObject]](../models/listentitlementgrantsobject.md) | :heavy_minus_sign:                                                                       | N/A                                                                                      |
| `data`                                                                                   | List[[models.Grant](../models/grant.md)]                                                 | :heavy_check_mark:                                                                       | N/A                                                                                      |
| `pagination`                                                                             | [models.OffsetPagination](../models/offsetpagination.md)                                 | :heavy_check_mark:                                                                       | Offset-based pagination response.                                                        |