# MeCredential

The credential of the call. clientId is set for an OAuth token and apiKeyId for an API key.


## Fields

| Field                                                    | Type                                                     | Required                                                 | Description                                              |
| -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- | -------------------------------------------------------- |
| `type`                                                   | [models.MeCredentialType](../models/mecredentialtype.md) | :heavy_check_mark:                                       | N/A                                                      |
| `client_id`                                              | *Optional[str]*                                          | :heavy_minus_sign:                                       | The OAuth client of the token.                           |
| `api_key_id`                                             | *Optional[str]*                                          | :heavy_minus_sign:                                       | The API key of the call.                                 |