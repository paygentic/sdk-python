# LineCalculationResult

Equal to the line's stored amount, quantity and unit price.


## Fields

| Field                                                                                              | Type                                                                                               | Required                                                                                           | Description                                                                                        |
| -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| `amount`                                                                                           | *str*                                                                                              | :heavy_check_mark:                                                                                 | The line's amount before tax.                                                                      |
| `quantity`                                                                                         | *Nullable[str]*                                                                                    | :heavy_check_mark:                                                                                 | The line's quantity.                                                                               |
| `unit_price`                                                                                       | *Nullable[str]*                                                                                    | :heavy_check_mark:                                                                                 | The line's unit price. It can be rounded, so quantity times unit price can differ from the amount. |