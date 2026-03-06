# paygentic-sdk

Developer-friendly & type-safe Python SDK specifically catered to leverage *paygentic-sdk* API.

[![Built by Speakeasy](https://img.shields.io/badge/Built_by-SPEAKEASY-374151?style=for-the-badge&labelColor=f3f4f6)](https://www.speakeasy.com/?utm_source=paygentic-sdk&utm_campaign=python)
[![License: MIT](https://img.shields.io/badge/LICENSE_//_MIT-3b5bdb?style=for-the-badge&labelColor=eff6ff)](https://opensource.org/licenses/MIT)


<br /><br />
> [!IMPORTANT]
> This SDK is not yet ready for production use. To complete setup please follow the steps outlined in your [workspace](https://app.speakeasy.com/org/paygentic/default). Delete this section before > publishing to a package manager.

<!-- Start Summary [summary] -->
## Summary

Paygentic API: The Paygentic API provides a comprehensive platform for building and scaling monetization infrastructure.

## Authentication
All API requests require authentication using an API key passed in the `Authorization` header:
```
Authorization: Bearer YOUR_API_KEY
```

## Base URL
All API requests should be made to:
```
https://api.paygentic.io/v0
```
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [paygentic-sdk](#paygentic-sdk)
  * [Authentication](#authentication)
  * [Base URL](#base-url)
  * [SDK Installation](#sdk-installation)
  * [IDE Support](#ide-support)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication-1)
  * [Available Resources and Operations](#available-resources-and-operations)
  * [Retries](#retries)
  * [Error Handling](#error-handling)
  * [Server Selection](#server-selection)
  * [Custom HTTP Client](#custom-http-client)
  * [Resource Management](#resource-management)
  * [Debugging](#debugging)
* [Development](#development)
  * [Maturity](#maturity)
  * [Contributions](#contributions)

<!-- End Table of Contents [toc] -->

<!-- Start SDK Installation [installation] -->
## SDK Installation

> [!NOTE]
> **Python version upgrade policy**
>
> Once a Python version reaches its [official end of life date](https://devguide.python.org/versions/), a 3-month grace period is provided for users to upgrade. Following this grace period, the minimum python version supported in the SDK will be updated.

The SDK can be installed with *uv*, *pip*, or *poetry* package managers.

### uv

*uv* is a fast Python package installer and resolver, designed as a drop-in replacement for pip and pip-tools. It's recommended for its speed and modern Python tooling capabilities.

```bash
uv add paygentic-sdk
```

### PIP

*PIP* is the default package installer for Python, enabling easy installation and management of packages from PyPI via the command line.

```bash
pip install paygentic-sdk
```

### Poetry

*Poetry* is a modern tool that simplifies dependency management and package publishing by using a single `pyproject.toml` file to handle project metadata and dependencies.

```bash
poetry add paygentic-sdk
```

### Shell and script usage with `uv`

You can use this SDK in a Python shell with [uv](https://docs.astral.sh/uv/) and the `uvx` command that comes with it like so:

```shell
uvx --from paygentic-sdk python
```

It's also possible to write a standalone Python script without needing to set up a whole project like so:

```python
#!/usr/bin/env -S uv run --script
# /// script
# requires-python = ">=3.10"
# dependencies = [
#     "paygentic-sdk",
# ]
# ///

from paygentic_sdk import Paygentic

sdk = Paygentic(
  # SDK arguments
)

# Rest of script here...
```

Once that is saved to a file, you can run it with `uv run script.py` where
`script.py` can be replaced with the actual file name.
<!-- End SDK Installation [installation] -->

<!-- Start IDE Support [idesupport] -->
## IDE Support

### PyCharm

Generally, the SDK will work well with most IDEs out of the box. However, when using PyCharm, you can enjoy much better integration with Pydantic by installing an additional plugin.

- [PyCharm Pydantic Plugin](https://docs.pydantic.dev/latest/integrations/pycharm/)
<!-- End IDE Support [idesupport] -->

<!-- Start SDK Example Usage [usage] -->
## SDK Example Usage

### Example

```python
# Synchronous Example
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter")

    # Handle response
    print(res)
```

</br>

The same SDK client can also be used to make asynchronous requests by importing asyncio.

```python
# Asynchronous Example
import asyncio
import os
from paygentic_sdk import Paygentic

async def main():

    async with Paygentic(
        bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
    ) as paygentic:

        res = await paygentic.billable_metrics.create_async(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter")

        # Handle response
        print(res)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name          | Type | Scheme      | Environment Variable    |
| ------------- | ---- | ----------- | ----------------------- |
| `bearer_auth` | http | HTTP Bearer | `PAYGENTIC_BEARER_AUTH` |

To authenticate with the API the `bearer_auth` parameter must be set when initializing the SDK client instance. For example:
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter")

    # Handle response
    print(res)

```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [BillableMetrics](docs/sdks/billablemetrics/README.md)

* [create](docs/sdks/billablemetrics/README.md#create) - Create
* [list](docs/sdks/billablemetrics/README.md#list) - List
* [get](docs/sdks/billablemetrics/README.md#get) - Get
* [update](docs/sdks/billablemetrics/README.md#update) - Update
* [meter](docs/sdks/billablemetrics/README.md#meter) - Query Meter Usage

### [Customers](docs/sdks/customers/README.md)

* [list](docs/sdks/customers/README.md#list) - List by Merchant
* [create](docs/sdks/customers/README.md#create) - Create
* [get](docs/sdks/customers/README.md#get) - Get
* [delete](docs/sdks/customers/README.md#delete) - Delete
* [update](docs/sdks/customers/README.md#update) - Update

### [Disputes](docs/sdks/disputes/README.md)

* [create](docs/sdks/disputes/README.md#create) - Create
* [list](docs/sdks/disputes/README.md#list) - List

### [Entitlements](docs/sdks/entitlements/README.md)

* [list](docs/sdks/entitlements/README.md#list) - List Entitlements
* [issue](docs/sdks/entitlements/README.md#issue) - Issue Entitlement
* [get](docs/sdks/entitlements/README.md#get) - Get Entitlement

### [EntitlementsV0](docs/sdks/entitlementsv0/README.md)

* [list_active](docs/sdks/entitlementsv0/README.md#list_active) - List by Customer
* [create](docs/sdks/entitlementsv0/README.md#create) - Create

### [Events](docs/sdks/events/README.md)

* [ingest](docs/sdks/events/README.md#ingest) - Ingest Event

### [Features](docs/sdks/features/README.md)

* [list](docs/sdks/features/README.md#list) - List
* [create](docs/sdks/features/README.md#create) - Create
* [get](docs/sdks/features/README.md#get) - Get
* [update](docs/sdks/features/README.md#update) - Update
* [delete](docs/sdks/features/README.md#delete) - Delete

### [Fees](docs/sdks/fees/README.md)

* [create](docs/sdks/fees/README.md#create) - Create
* [list](docs/sdks/fees/README.md#list) - List
* [get](docs/sdks/fees/README.md#get) - Get
* [update](docs/sdks/fees/README.md#update) - Update
* [delete](docs/sdks/fees/README.md#delete) - Delete
* [get_price](docs/sdks/fees/README.md#get_price) - Get Fee Price

### [InvoicesV2](docs/sdks/invoicesv2/README.md)

* [list](docs/sdks/invoicesv2/README.md#list) - List
* [get](docs/sdks/invoicesv2/README.md#get) - Get
* [get_line_items](docs/sdks/invoicesv2/README.md#get_line_items) - Get Line Items

### [Payments](docs/sdks/payments/README.md)

* [list](docs/sdks/payments/README.md#list) - List Payments
* [create](docs/sdks/payments/README.md#create) - Create Payment
* [get](docs/sdks/payments/README.md#get) - Get Payment

### [Plans](docs/sdks/plans/README.md)

* [create](docs/sdks/plans/README.md#create) - Create
* [list](docs/sdks/plans/README.md#list) - List
* [list_available](docs/sdks/plans/README.md#list_available) - List Available Plans
* [get](docs/sdks/plans/README.md#get) - Get
* [update](docs/sdks/plans/README.md#update) - Update

### [Prices](docs/sdks/prices/README.md)

* [create](docs/sdks/prices/README.md#create) - Create
* [list](docs/sdks/prices/README.md#list) - List
* [get](docs/sdks/prices/README.md#get) - Get
* [update](docs/sdks/prices/README.md#update) - Update
* [delete](docs/sdks/prices/README.md#delete) - Delete

### [Products](docs/sdks/products/README.md)

* [create](docs/sdks/products/README.md#create) - Create
* [list](docs/sdks/products/README.md#list) - List
* [get](docs/sdks/products/README.md#get) - Get
* [update](docs/sdks/products/README.md#update) - Update

### [Revenue](docs/sdks/revenue/README.md)

* [get](docs/sdks/revenue/README.md#get) - Get revenue time series

### [Sources](docs/sdks/sources/README.md)

* [create](docs/sdks/sources/README.md#create) - Create
* [list](docs/sdks/sources/README.md#list) - List
* [get](docs/sdks/sources/README.md#get) - Get
* [update](docs/sdks/sources/README.md#update) - Update

### [Sources.Events](docs/sdks/sourcesevents/README.md)

* [list](docs/sdks/sourcesevents/README.md#list) - List Events
* [approve](docs/sdks/sourcesevents/README.md#approve) - Approve
* [reject](docs/sdks/sourcesevents/README.md#reject) - Reject
* [bulk_approve](docs/sdks/sourcesevents/README.md#bulk_approve) - Bulk Approve
* [bulk_reject](docs/sdks/sourcesevents/README.md#bulk_reject) - Bulk Reject

### [Sources.Rules](docs/sdks/rules/README.md)

* [list](docs/sdks/rules/README.md#list) - List Rules
* [create](docs/sdks/rules/README.md#create) - Create Rule
* [get](docs/sdks/rules/README.md#get) - Get Rule
* [update](docs/sdks/rules/README.md#update) - Update Rule
* [delete](docs/sdks/rules/README.md#delete) - Delete Rule

### [Subscriptions](docs/sdks/subscriptions/README.md)

* [list](docs/sdks/subscriptions/README.md#list) - List
* [create](docs/sdks/subscriptions/README.md#create) - Create
* [get](docs/sdks/subscriptions/README.md#get) - Get
* [generate_portal_link](docs/sdks/subscriptions/README.md#generate_portal_link) - Generate Portal Link
* [terminate](docs/sdks/subscriptions/README.md#terminate) - Terminate

### [TestClocks](docs/sdks/testclocks/README.md)

* [list](docs/sdks/testclocks/README.md#list) - List
* [create](docs/sdks/testclocks/README.md#create) - Create
* [get](docs/sdks/testclocks/README.md#get) - Get
* [advance](docs/sdks/testclocks/README.md#advance) - Advance
* [delete](docs/sdks/testclocks/README.md#delete) - Delete

### [UsageEvents](docs/sdks/usageevents/README.md)

* [create](docs/sdks/usageevents/README.md#create) - Create
* [list](docs/sdks/usageevents/README.md#list) - List
* [get](docs/sdks/usageevents/README.md#get) - Get
* [refund](docs/sdks/usageevents/README.md#refund) - Refund
* [batch_create](docs/sdks/usageevents/README.md#batch_create) - Batch Create

### [Users](docs/sdks/users/README.md)

* [get](docs/sdks/users/README.md#get) - Get
* [update](docs/sdks/users/README.md#update) - Update

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply provide a `RetryConfig` object to the call:
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import BackoffStrategy, RetryConfig


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter",
        RetryConfig("backoff", BackoffStrategy(1, 50, 1.1, 100), False))

    # Handle response
    print(res)

```

If you'd like to override the default retry strategy for all operations that support retries, you can use the `retry_config` optional parameter when initializing the SDK:
```python
import os
from paygentic_sdk import Paygentic
from paygentic_sdk.utils import BackoffStrategy, RetryConfig


with Paygentic(
    retry_config=RetryConfig("backoff", BackoffStrategy(1, 50, 1.1, 100), False),
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter")

    # Handle response
    print(res)

```
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

[`PaygenticError`](./src/paygentic_sdk/errors/paygenticerror.py) is the base class for all HTTP error responses. It has the following properties:

| Property           | Type             | Description                                                                             |
| ------------------ | ---------------- | --------------------------------------------------------------------------------------- |
| `err.message`      | `str`            | Error message                                                                           |
| `err.status_code`  | `int`            | HTTP response status code eg `404`                                                      |
| `err.headers`      | `httpx.Headers`  | HTTP response headers                                                                   |
| `err.body`         | `str`            | HTTP body. Can be empty string if no body is returned.                                  |
| `err.raw_response` | `httpx.Response` | Raw HTTP response                                                                       |
| `err.data`         |                  | Optional. Some errors may contain structured data. [See Error Classes](#error-classes). |

### Example
```python
import os
from paygentic_sdk import Paygentic, errors


with Paygentic(
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:
    res = None
    try:

        res = paygentic.billable_metrics.create(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter")

        # Handle response
        print(res)


    except errors.PaygenticError as e:
        # The base class for HTTP error responses
        print(e.message)
        print(e.status_code)
        print(e.body)
        print(e.headers)
        print(e.raw_response)

        # Depending on the method different errors may be thrown
        if isinstance(e, errors.Error):
            print(e.data.error)  # Optional[str]
            print(e.data.message)  # str
            print(e.data.details)  # Optional[Dict[str, Any]]
```

### Error Classes
**Primary errors:**
* [`PaygenticError`](./src/paygentic_sdk/errors/paygenticerror.py): The base class for HTTP error responses.
  * [`Error`](./src/paygentic_sdk/errors/error.py): Generic error.

<details><summary>Less common errors (8)</summary>

<br />

**Network errors:**
* [`httpx.RequestError`](https://www.python-httpx.org/exceptions/#httpx.RequestError): Base class for request errors.
    * [`httpx.ConnectError`](https://www.python-httpx.org/exceptions/#httpx.ConnectError): HTTP client was unable to make a request to a server.
    * [`httpx.TimeoutException`](https://www.python-httpx.org/exceptions/#httpx.TimeoutException): HTTP request timed out.


**Inherit from [`PaygenticError`](./src/paygentic_sdk/errors/paygenticerror.py)**:
* [`ValidationError`](./src/paygentic_sdk/errors/validationerror.py): Bad Request - The request could not be understood or was missing required parameters. Status code `400`. Applicable to 48 of 81 methods.*
* [`DeleteCustomerConflictError`](./src/paygentic_sdk/errors/deletecustomerconflicterror.py): Customer cannot be deleted due to active dependencies. Status code `409`. Applicable to 1 of 81 methods.*
* [`DeleteFeeConflictError`](./src/paygentic_sdk/errors/deletefeeconflicterror.py): Fee cannot be deleted because it has associated prices. Status code `409`. Applicable to 1 of 81 methods.*
* [`ResponseValidationError`](./src/paygentic_sdk/errors/responsevalidationerror.py): Type mismatch between the response data and the expected Pydantic model. Provides access to the Pydantic validation error via the `cause` attribute.

</details>

\* Check [the method documentation](#available-resources-and-operations) to see if the error is applicable.
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Override Server URL Per-Client

The default server can be overridden globally by passing a URL to the `server_url: str` optional parameter when initializing the SDK client instance. For example:
```python
import os
from paygentic_sdk import Paygentic


with Paygentic(
    server_url="https://api.paygentic.io",
    bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
) as paygentic:

    res = paygentic.billable_metrics.create(aggregation="SUM", description="orange daily out slow nor smoothly", merchant_id="<id>", name="<value>", product_id="<id>", unit="meter")

    # Handle response
    print(res)

```
<!-- End Server Selection [server] -->

<!-- Start Custom HTTP Client [http-client] -->
## Custom HTTP Client

The Python SDK makes API calls using the [httpx](https://www.python-httpx.org/) HTTP library.  In order to provide a convenient way to configure timeouts, cookies, proxies, custom headers, and other low-level configuration, you can initialize the SDK client with your own HTTP client instance.
Depending on whether you are using the sync or async version of the SDK, you can pass an instance of `HttpClient` or `AsyncHttpClient` respectively, which are Protocol's ensuring that the client has the necessary methods to make API calls.
This allows you to wrap the client with your own custom logic, such as adding custom headers, logging, or error handling, or you can just pass an instance of `httpx.Client` or `httpx.AsyncClient` directly.

For example, you could specify a header for every request that this sdk makes as follows:
```python
from paygentic_sdk import Paygentic
import httpx

http_client = httpx.Client(headers={"x-custom-header": "someValue"})
s = Paygentic(client=http_client)
```

or you could wrap the client with your own custom logic:
```python
from paygentic_sdk import Paygentic
from paygentic_sdk.httpclient import AsyncHttpClient
import httpx

class CustomClient(AsyncHttpClient):
    client: AsyncHttpClient

    def __init__(self, client: AsyncHttpClient):
        self.client = client

    async def send(
        self,
        request: httpx.Request,
        *,
        stream: bool = False,
        auth: Union[
            httpx._types.AuthTypes, httpx._client.UseClientDefault, None
        ] = httpx.USE_CLIENT_DEFAULT,
        follow_redirects: Union[
            bool, httpx._client.UseClientDefault
        ] = httpx.USE_CLIENT_DEFAULT,
    ) -> httpx.Response:
        request.headers["Client-Level-Header"] = "added by client"

        return await self.client.send(
            request, stream=stream, auth=auth, follow_redirects=follow_redirects
        )

    def build_request(
        self,
        method: str,
        url: httpx._types.URLTypes,
        *,
        content: Optional[httpx._types.RequestContent] = None,
        data: Optional[httpx._types.RequestData] = None,
        files: Optional[httpx._types.RequestFiles] = None,
        json: Optional[Any] = None,
        params: Optional[httpx._types.QueryParamTypes] = None,
        headers: Optional[httpx._types.HeaderTypes] = None,
        cookies: Optional[httpx._types.CookieTypes] = None,
        timeout: Union[
            httpx._types.TimeoutTypes, httpx._client.UseClientDefault
        ] = httpx.USE_CLIENT_DEFAULT,
        extensions: Optional[httpx._types.RequestExtensions] = None,
    ) -> httpx.Request:
        return self.client.build_request(
            method,
            url,
            content=content,
            data=data,
            files=files,
            json=json,
            params=params,
            headers=headers,
            cookies=cookies,
            timeout=timeout,
            extensions=extensions,
        )

s = Paygentic(async_client=CustomClient(httpx.AsyncClient()))
```
<!-- End Custom HTTP Client [http-client] -->

<!-- Start Resource Management [resource-management] -->
## Resource Management

The `Paygentic` class implements the context manager protocol and registers a finalizer function to close the underlying sync and async HTTPX clients it uses under the hood. This will close HTTP connections, release memory and free up other resources held by the SDK. In short-lived Python programs and notebooks that make a few SDK method calls, resource management may not be a concern. However, in longer-lived programs, it is beneficial to create a single SDK instance via a [context manager][context-manager] and reuse it across the application.

[context-manager]: https://docs.python.org/3/reference/datamodel.html#context-managers

```python
import os
from paygentic_sdk import Paygentic
def main():

    with Paygentic(
        bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
    ) as paygentic:
        # Rest of application here...


# Or when using async:
async def amain():

    async with Paygentic(
        bearer_auth=os.getenv("PAYGENTIC_BEARER_AUTH", ""),
    ) as paygentic:
        # Rest of application here...
```
<!-- End Resource Management [resource-management] -->

<!-- Start Debugging [debug] -->
## Debugging

You can setup your SDK to emit debug logs for SDK requests and responses.

You can pass your own logger class directly into your SDK.
```python
from paygentic_sdk import Paygentic
import logging

logging.basicConfig(level=logging.DEBUG)
s = Paygentic(debug_logger=logging.getLogger("paygentic_sdk"))
```

You can also enable a default debug logger by setting an environment variable `PAYGENTIC_DEBUG` to true.
<!-- End Debugging [debug] -->

<!-- Placeholder for Future Speakeasy SDK Sections -->

# Development

## Maturity

This SDK is in beta, and there may be breaking changes between versions without a major version update. Therefore, we recommend pinning usage
to a specific package version. This way, you can install the same version each time without breaking changes unless you are intentionally
looking for the latest version.

## Contributions

While we value open-source contributions to this SDK, this library is generated programmatically. Any manual changes added to internal files will be overwritten on the next generation. 
We look forward to hearing your feedback. Feel free to open a PR or an issue with a proof of concept and we'll do our best to include it in a future release. 

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=paygentic-sdk&utm_campaign=python)
