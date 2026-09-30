# Metrics

## Overview

Pre-aggregated permit counts and valuation from a nightly rollup. Use these instead of paging through search results to count them: they answer 'how many' and 'is it trending' in one millisecond-scale call. Developer plan and above.

### Available Operations

* [metrics_monthly](#metrics_monthly) - Metrics Monthly
* [metrics_current](#metrics_current) - Metrics Current
* [metrics_cities](#metrics_cities) - Metrics Cities

## metrics_monthly

Monthly permit counts and total valuation for a city/state/category.

Available on the Developer plan and above (see /v1/billing/plans for current pricing).

Served from a nightly rollup, so it answers in milliseconds where the equivalent
search-and-count takes seconds. At least one of `state` or `city` is required: an
unfiltered national series would be a different (and much larger) product.

### Example Usage

<!-- UsageSnippet language="python" operationID="metrics_monthly" method="get" path="/v1/metrics/monthly" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.metrics.metrics_monthly(months=24)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `state`                                                             | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | Two-letter state code, e.g. FL                                      |
| `city`                                                              | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | City name; case-insensitive                                         |
| `category`                                                          | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | Permit category, e.g. ROOFING                                       |
| `months`                                                            | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | How many trailing months to return                                  |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.FeatureLockedError      | 403                            | application/json               |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## metrics_current

Category breakdown over a trailing window — the 'what is happening here now' view.

Available on the Developer plan and above (see /v1/billing/plans for current pricing).

### Example Usage

<!-- UsageSnippet language="python" operationID="metrics_current" method="get" path="/v1/metrics/current" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.metrics.metrics_current(days=90)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `state`                                                             | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | N/A                                                                 |
| `city`                                                              | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | N/A                                                                 |
| `days`                                                              | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | Trailing window. Rounded to whole months by the rollup.             |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.FeatureLockedError      | 403                            | application/json               |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## metrics_cities

Busiest cities in a state — the ranking customers were building by hand.

Available on the Developer plan and above (see /v1/billing/plans for current pricing).

### Example Usage

<!-- UsageSnippet language="python" operationID="metrics_cities" method="get" path="/v1/metrics/cities" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.metrics.metrics_cities(state="Virginia", months=12, limit=50)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `state`                                                             | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `category`                                                          | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | N/A                                                                 |
| `months`                                                            | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `limit`                                                             | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.FeatureLockedError      | 403                            | application/json               |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |