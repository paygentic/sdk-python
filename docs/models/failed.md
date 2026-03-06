# Failed


## Fields

| Field                                                   | Type                                                    | Required                                                | Description                                             |
| ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- | ------------------------------------------------------- |
| `error`                                                 | *str*                                                   | :heavy_check_mark:                                      | Error message describing why the event failed           |
| `idempotency_key`                                       | *str*                                                   | :heavy_check_mark:                                      | Idempotency key of the failed event for identification  |
| `index`                                                 | *int*                                                   | :heavy_check_mark:                                      | Index of the failed event in the original request array |