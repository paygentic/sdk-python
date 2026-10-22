# LineCalculationInputPrice

`priced` only: the price as a function, and its source.


## Fields

| Field                                                                                       | Type                                                                                        | Required                                                                                    | Description                                                                                 |
| ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| `fn`                                                                                        | [models.LineCalculationPriceFn](../models/linecalculationpricefn.md)                        | :heavy_check_mark:                                                                          | A price as a function from quantity to money. A new model may carry fields not listed here. |
| `source`                                                                                    | *str*                                                                                       | :heavy_check_mark:                                                                          | The key of the source in `sources` that stated the price.                                   |