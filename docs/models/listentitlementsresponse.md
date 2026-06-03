# ListEntitlementsResponse

Successfully retrieved the list of entitlements for the customer.


## Fields

| Field                                                                          | Type                                                                           | Required                                                                       | Description                                                                    |
| ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------ |
| `object`                                                                       | [Optional[models.ListEntitlementsObject]](../models/listentitlementsobject.md) | :heavy_minus_sign:                                                             | N/A                                                                            |
| `data`                                                                         | List[[models.EntitlementListItem](../models/entitlementlistitem.md)]           | :heavy_check_mark:                                                             | Array of entitlement list items. The shape of each item varies by featureType. |
| `pagination`                                                                   | [models.OffsetPagination](../models/offsetpagination.md)                       | :heavy_check_mark:                                                             | Offset-based pagination response.                                              |