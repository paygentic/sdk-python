# ValidationError


## Fields

| Field                                                | Type                                                 | Required                                             | Description                                          |
| ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- | ---------------------------------------------------- |
| `error`                                              | [Optional[models.ErrorEnum]](../models/errorenum.md) | :heavy_minus_sign:                                   | Error type indicating validation failure             |
| `message`                                            | *str*                                                | :heavy_check_mark:                                   | Human-readable error message                         |
| `errors`                                             | List[[models.Error](../models/error.md)]             | :heavy_check_mark:                                   | Array of field-specific validation errors            |