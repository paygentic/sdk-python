# ListEntitlementGrantsRequest


## Fields

| Field                                                  | Type                                                   | Required                                               | Description                                            |
| ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ | ------------------------------------------------------ |
| `entitlement_id`                                       | *str*                                                  | :heavy_check_mark:                                     | The unique identifier of the entitlement.              |
| `limit`                                                | *Optional[int]*                                        | :heavy_minus_sign:                                     | Maximum number of grants to return per page.           |
| `offset`                                               | *Optional[int]*                                        | :heavy_minus_sign:                                     | Number of grants to skip.                              |
| `include_voided`                                       | *Optional[bool]*                                       | :heavy_minus_sign:                                     | When true, voided grants are included in the response. |