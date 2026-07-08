# permitstack

Developer-friendly & type-safe Python SDK specifically catered to leverage *permitstack* API.

[![Built by Speakeasy](https://img.shields.io/badge/Built_by-SPEAKEASY-374151?style=for-the-badge&labelColor=f3f4f6)](https://www.speakeasy.com/?utm_source=permitstack&utm_campaign=python)
[![License: Apache 2.0](https://img.shields.io/badge/License-Apache_2.0-blue.svg?style=for-the-badge&labelColor=eff6ff)](https://opensource.org/licenses/Apache-2.0)



<!-- Start Summary [summary] -->
## Summary

PermitStack: 
## PermitStack Building Permit API

Access 63M+ building permits across 7,000+ U.S. cities in all 50 states (615 active data sources spanning counties and statewide feeds, plus ~74 historical archives), updated daily from official open data portals.

### Getting started
1. Sign up at [permit-stack.com](https://permit-stack.com/#pricing) for a free API key (100 req/day)
2. Pass your key as `X-API-Key` header on every request
3. See the `/v1/permits/search` endpoint to get started

### Rate limits
Tier       | Requests/min | Requests/day
-----------|--------------|-------------
Free       | 30           | 100
Indie      | 30           | 1,000
Hobbyist   | 30           | 2,500
Developer  | 60           | 10,000
Business    | 200          | 100,000
Growth     | 500          | 500,000

### Support
support@permit-stack.com
<!-- End Summary [summary] -->

<!-- Start Table of Contents [toc] -->
## Table of Contents
<!-- $toc-max-depth=2 -->
* [permitstack](#permitstack)
  * [PermitStack Building Permit API](#permitstack-building-permit-api)
  * [SDK Installation](#sdk-installation)
  * [IDE Support](#ide-support)
  * [SDK Example Usage](#sdk-example-usage)
  * [Authentication](#authentication)
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

> [!TIP]
> To finish publishing your SDK to PyPI you must [run your first generation action](https://www.speakeasy.com/docs/github-setup#step-by-step-guide).


> [!NOTE]
> **Python version upgrade policy**
>
> Once a Python version reaches its [official end of life date](https://devguide.python.org/versions/), a 3-month grace period is provided for users to upgrade. Following this grace period, the minimum python version supported in the SDK will be updated.

The SDK can be installed with *uv*, *pip*, or *poetry* package managers.

### uv

*uv* is a fast Python package installer and resolver, designed as a drop-in replacement for pip and pip-tools. It's recommended for its speed and modern Python tooling capabilities.

```bash
uv add git+<UNSET>.git
```

### PIP

*PIP* is the default package installer for Python, enabling easy installation and management of packages from PyPI via the command line.

```bash
pip install git+<UNSET>.git
```

### Poetry

*Poetry* is a modern tool that simplifies dependency management and package publishing by using a single `pyproject.toml` file to handle project metadata and dependencies.

```bash
poetry add git+<UNSET>.git
```

### Shell and script usage with `uv`

You can use this SDK in a Python shell with [uv](https://docs.astral.sh/uv/) and the `uvx` command that comes with it like so:

```shell
uvx --from permitstack python
```

It's also possible to write a standalone Python script without needing to set up a whole project like so:

```python
#!/usr/bin/env -S uv run --script
# /// script
# requires-python = ">=3.10"
# dependencies = [
#     "permitstack",
# ]
# ///

from permitstack import Permitstack

sdk = Permitstack(
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
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.health.health_check()

    # Handle response
    print(res)
```

</br>

The same SDK client can also be used to make asynchronous requests by importing asyncio.

```python
# Asynchronous Example
import asyncio
import os
from permitstack import Permitstack

async def main():

    async with Permitstack(
        api_key=os.getenv("PERMITSTACK_API_KEY", ""),
    ) as p_client:

        res = await p_client.health.health_check_async()

        # Handle response
        print(res)

asyncio.run(main())
```
<!-- End SDK Example Usage [usage] -->

<!-- Start Authentication [security] -->
## Authentication

### Per-Client Security Schemes

This SDK supports the following security scheme globally:

| Name      | Type   | Scheme  | Environment Variable  |
| --------- | ------ | ------- | --------------------- |
| `api_key` | apiKey | API key | `PERMITSTACK_API_KEY` |

To authenticate with the API the `api_key` parameter must be set when initializing the SDK client instance. For example:
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.health.health_check()

    # Handle response
    print(res)

```
<!-- End Authentication [security] -->

<!-- Start Available Resources and Operations [operations] -->
## Available Resources and Operations

<details open>
<summary>Available methods</summary>

### [Contractors](docs/sdks/contractors/README.md)

* [search_contractors](docs/sdks/contractors/README.md#search_contractors) - Search Contractors
* [get_contractor](docs/sdks/contractors/README.md#get_contractor) - Get Contractor
* [get_contractor_permits](docs/sdks/contractors/README.md#get_contractor_permits) - Get Contractor Permits

### [Health](docs/sdks/health/README.md)

* [health_check](docs/sdks/health/README.md#health_check) - Health Check
* [public_stats](docs/sdks/health/README.md#public_stats) - Public Stats

### [Permits](docs/sdks/permits/README.md)

* [search_permits](docs/sdks/permits/README.md#search_permits) - Search Permits
* [export_permits](docs/sdks/permits/README.md#export_permits) - Export Permits
* [list_permit_events](docs/sdks/permits/README.md#list_permit_events) - List Permit Events
* [get_permit](docs/sdks/permits/README.md#get_permit) - Get Permit
* [get_permits_by_address](docs/sdks/permits/README.md#get_permits_by_address) - Get Permits By Address
* [get_coverage_stats](docs/sdks/permits/README.md#get_coverage_stats) - Get Coverage Stats
* [list_plays](docs/sdks/permits/README.md#list_plays) - List Plays
* [battery_retrofit_candidates](docs/sdks/permits/README.md#battery_retrofit_candidates) - Battery Retrofit Candidates
* [orphan_recovery](docs/sdks/permits/README.md#orphan_recovery) - Orphan Recovery

### [PropertyHistory](docs/sdks/propertyhistory/README.md)

* [get_property_history](docs/sdks/propertyhistory/README.md#get_property_history) - Get Property History
* [get_property_by_parcel](docs/sdks/propertyhistory/README.md#get_property_by_parcel) - Get Property By Parcel

### [Webhooks](docs/sdks/webhooks/README.md)

* [list_webhooks](docs/sdks/webhooks/README.md#list_webhooks) - List Webhooks
* [create_webhook](docs/sdks/webhooks/README.md#create_webhook) - Create Webhook
* [delete_webhook](docs/sdks/webhooks/README.md#delete_webhook) - Delete Webhook
* [test_webhook](docs/sdks/webhooks/README.md#test_webhook) - Test Webhook
* [get_webhook_secret](docs/sdks/webhooks/README.md#get_webhook_secret) - Get Webhook Secret

</details>
<!-- End Available Resources and Operations [operations] -->

<!-- Start Retries [retries] -->
## Retries

Some of the endpoints in this SDK support retries. If you use the SDK without any configuration, it will fall back to the default retry strategy provided by the API. However, the default retry strategy can be overridden on a per-operation basis, or across the entire SDK.

To change the default retry strategy for a single API call, simply provide a `RetryConfig` object to the call:
```python
import os
from permitstack import Permitstack
from permitstack.utils import BackoffStrategy, RetryConfig


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.health.health_check(,
        RetryConfig("backoff", BackoffStrategy(1, 50, 1.1, 100), False))

    # Handle response
    print(res)

```

If you'd like to override the default retry strategy for all operations that support retries, you can use the `retry_config` optional parameter when initializing the SDK:
```python
import os
from permitstack import Permitstack
from permitstack.utils import BackoffStrategy, RetryConfig


with Permitstack(
    retry_config=RetryConfig("backoff", BackoffStrategy(1, 50, 1.1, 100), False),
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.health.health_check()

    # Handle response
    print(res)

```
<!-- End Retries [retries] -->

<!-- Start Error Handling [errors] -->
## Error Handling

[`PermitstackError`](./src/permitstack/errors/permitstackerror.py) is the base class for all HTTP error responses. It has the following properties:

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
from permitstack import Permitstack, errors


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:
    res = None
    try:

        res = p_client.permits.search_permits(radius_miles=5, record_kind="permit", page=1, per_page=25)

        # Handle response
        print(res)


    except errors.PermitstackError as e:
        # The base class for HTTP error responses
        print(e.message)
        print(e.status_code)
        print(e.body)
        print(e.headers)
        print(e.raw_response)

        # Depending on the method different errors may be thrown
        if isinstance(e, errors.HTTPValidationError):
            print(e.data.detail)  # Optional[List[models.ValidationError]]
```

### Error Classes
**Primary error:**
* [`PermitstackError`](./src/permitstack/errors/permitstackerror.py): The base class for HTTP error responses.

<details><summary>Less common errors (6)</summary>

<br />

**Network errors:**
* [`httpx.RequestError`](https://www.python-httpx.org/exceptions/#httpx.RequestError): Base class for request errors.
    * [`httpx.ConnectError`](https://www.python-httpx.org/exceptions/#httpx.ConnectError): HTTP client was unable to make a request to a server.
    * [`httpx.TimeoutException`](https://www.python-httpx.org/exceptions/#httpx.TimeoutException): HTTP request timed out.


**Inherit from [`PermitstackError`](./src/permitstack/errors/permitstackerror.py)**:
* [`HTTPValidationError`](./src/permitstack/errors/httpvalidationerror.py): Validation Error. Status code `422`. Applicable to 16 of 21 methods.*
* [`ResponseValidationError`](./src/permitstack/errors/responsevalidationerror.py): Type mismatch between the response data and the expected Pydantic model. Provides access to the Pydantic validation error via the `cause` attribute.

</details>

\* Check [the method documentation](#available-resources-and-operations) to see if the error is applicable.
<!-- End Error Handling [errors] -->

<!-- Start Server Selection [server] -->
## Server Selection

### Override Server URL Per-Client

The default server can be overridden globally by passing a URL to the `server_url: str` optional parameter when initializing the SDK client instance. For example:
```python
import os
from permitstack import Permitstack


with Permitstack(
    server_url="https://api.permit-stack.com",
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.health.health_check()

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
from permitstack import Permitstack
import httpx

http_client = httpx.Client(headers={"x-custom-header": "someValue"})
s = Permitstack(client=http_client)
```

or you could wrap the client with your own custom logic:
```python
from permitstack import Permitstack
from permitstack.httpclient import AsyncHttpClient
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

s = Permitstack(async_client=CustomClient(httpx.AsyncClient()))
```
<!-- End Custom HTTP Client [http-client] -->

<!-- Start Resource Management [resource-management] -->
## Resource Management

The `Permitstack` class implements the context manager protocol and registers a finalizer function to close the underlying sync and async HTTPX clients it uses under the hood. This will close HTTP connections, release memory and free up other resources held by the SDK. In short-lived Python programs and notebooks that make a few SDK method calls, resource management may not be a concern. However, in longer-lived programs, it is beneficial to create a single SDK instance via a [context manager][context-manager] and reuse it across the application.

[context-manager]: https://docs.python.org/3/reference/datamodel.html#context-managers

```python
import os
from permitstack import Permitstack
def main():

    with Permitstack(
        api_key=os.getenv("PERMITSTACK_API_KEY", ""),
    ) as p_client:
        # Rest of application here...


# Or when using async:
async def amain():

    async with Permitstack(
        api_key=os.getenv("PERMITSTACK_API_KEY", ""),
    ) as p_client:
        # Rest of application here...
```
<!-- End Resource Management [resource-management] -->

<!-- Start Debugging [debug] -->
## Debugging

You can setup your SDK to emit debug logs for SDK requests and responses.

You can pass your own logger class directly into your SDK.
```python
from permitstack import Permitstack
import logging

logging.basicConfig(level=logging.DEBUG)
s = Permitstack(debug_logger=logging.getLogger("permitstack"))
```

You can also enable a default debug logger by setting an environment variable `PERMITSTACK_DEBUG` to true.
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

### SDK Created by [Speakeasy](https://www.speakeasy.com/?utm_source=permitstack&utm_campaign=python)
