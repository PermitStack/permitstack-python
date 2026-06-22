# PropertyHistory

## Overview

Get permit history for a specific address

### Available Operations

* [get_property_history](#get_property_history) - Get Property History
* [get_property_by_parcel](#get_property_by_parcel) - Get Property By Parcel

## get_property_history

Complete construction history + property profile for an address.

Matches every permit whose street address contains the supplied address;
pass `city`/`state`/`zip` to disambiguate the same street number across
metros. Returns a derived profile (permit timeline, category breakdown,
contractors, and underwriting signals such as solar/roof/pool age) plus
the paginated permit records.

An address with **no** permits returns `found: false` with an empty
profile (HTTP 200) — a clean property is a valid, useful answer, not an
error.

### Example Usage

<!-- UsageSnippet language="python" operationID="get_property_history" method="get" path="/v1/property/history" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.property_history.get_property_history(address="356 Von Bypass", page=1, per_page=50)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `address`                                                           | *str*                                                               | :heavy_check_mark:                                                  | Street address to look up (e.g. '123 Main St')                      |
| `city`                                                              | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | Optional city to disambiguate identical street addresses            |
| `state`                                                             | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | Optional 2-letter state code                                        |
| `zip`                                                               | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | Optional ZIP (prefix-matched)                                       |
| `page`                                                              | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `per_page`                                                          | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.PropertyHistoryResponse](../../models/propertyhistoryresponse.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## get_property_by_parcel

Complete construction history + property profile for a parcel / APN.

Looks up every permit whose source parcel number matches `parcel`, with
formatting ignored, so an APN from a county appraiser matches regardless of how
the permit feed punctuates it. Pass `state` to disambiguate the same parcel
number used by different counties. Returns the same profile shape as /history
(timeline, category breakdown, contractors, and roof/solar/HVAC age signals).

Parcel coverage spans the county / appraiser / GIS sources that publish a parcel
id; a handful of Accela-sourced jurisdictions omit parcel in their public export
and won't match here (use /property/history by address for those).

A parcel with **no** permits returns `found: false` (HTTP 200), not an error.

### Example Usage

<!-- UsageSnippet language="python" operationID="get_property_by_parcel" method="get" path="/v1/property/by-parcel" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.property_history.get_property_by_parcel(parcel="<value>", page=1, per_page=50)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                  | Type                                                                                                       | Required                                                                                                   | Description                                                                                                |
| ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------- |
| `parcel`                                                                                                   | *str*                                                                                                      | :heavy_check_mark:                                                                                         | Parcel number / APN / folio. Formatting is ignored — dashes, dots and spaces are stripped before matching. |
| `state`                                                                                                    | *OptionalNullable[str]*                                                                                    | :heavy_minus_sign:                                                                                         | Optional 2-letter state to disambiguate the same parcel number across counties                             |
| `page`                                                                                                     | *Optional[int]*                                                                                            | :heavy_minus_sign:                                                                                         | N/A                                                                                                        |
| `per_page`                                                                                                 | *Optional[int]*                                                                                            | :heavy_minus_sign:                                                                                         | N/A                                                                                                        |
| `retries`                                                                                                  | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                           | :heavy_minus_sign:                                                                                         | Configuration to override the default retry behavior of the client.                                        |

### Response

**[models.PropertyHistoryResponse](../../models/propertyhistoryresponse.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |