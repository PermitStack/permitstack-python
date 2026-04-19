# PropertyHistory

## Overview

Get permit history for a specific address

### Available Operations

* [get_property_history](#get_property_history) - Get Property History

## get_property_history

Get the complete construction history for a property address.

Returns all permits ever filed at or near this address, sorted by date.
Useful for insurance underwriting, real estate due diligence, and property valuation.

### Example Usage

<!-- UsageSnippet language="python" operationID="get_property_history" method="get" path="/v1/property/history" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.property_history.get_property_history(address="356 Von Bypass")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `address`                                                           | *str*                                                               | :heavy_check_mark:                                                  | Street address to look up                                           |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |