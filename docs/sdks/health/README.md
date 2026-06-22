# Health

## Overview

Service health checks

### Available Operations

* [health_check](#health_check) - Health Check
* [public_stats](#public_stats) - Public Stats

## health_check

Health Check

### Example Usage

<!-- UsageSnippet language="python" operationID="health_check" method="get" path="/health" -->
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

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## public_stats

Public stats endpoint — no auth required.
Returns aggregate coverage numbers for marketing/transparency.
Cached server-side for 30 minutes.

### Example Usage

<!-- UsageSnippet language="python" operationID="public_stats" method="get" path="/stats" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.health.public_stats()

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |