# Permits

## Overview

Search and retrieve building permits

### Available Operations

* [search_permits](#search_permits) - Search Permits
* [export_permits](#export_permits) - Export Permits
* [get_permit](#get_permit) - Get Permit
* [get_permits_by_address](#get_permits_by_address) - Get Permits By Address
* [get_coverage_stats](#get_coverage_stats) - Get Coverage Stats

## search_permits

Search Permits

### Example Usage

<!-- UsageSnippet language="python" operationID="search_permits" method="get" path="/v1/permits/search" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.permits.search_permits(radius_miles=5, record_kind="permit", page=1, per_page=25)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                      | Type                                                                                                           | Required                                                                                                       | Description                                                                                                    |
| -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| `zip_code`                                                                                                     | *OptionalNullable[str]*                                                                                        | :heavy_minus_sign:                                                                                             | 5-digit ZIP code                                                                                               |
| `city`                                                                                                         | *OptionalNullable[str]*                                                                                        | :heavy_minus_sign:                                                                                             | City name                                                                                                      |
| `state`                                                                                                        | *OptionalNullable[str]*                                                                                        | :heavy_minus_sign:                                                                                             | 2-letter state code                                                                                            |
| `jurisdiction`                                                                                                 | *OptionalNullable[str]*                                                                                        | :heavy_minus_sign:                                                                                             | Jurisdiction name (e.g. 'Wake County', 'Tacoma') or partial match                                              |
| `lat`                                                                                                          | *OptionalNullable[float]*                                                                                      | :heavy_minus_sign:                                                                                             | Latitude for radius search                                                                                     |
| `lng`                                                                                                          | *OptionalNullable[float]*                                                                                      | :heavy_minus_sign:                                                                                             | Longitude for radius search                                                                                    |
| `radius_miles`                                                                                                 | *Optional[float]*                                                                                              | :heavy_minus_sign:                                                                                             | Radius in miles (used with lat/lng)                                                                            |
| `category`                                                                                                     | *OptionalNullable[str]*                                                                                        | :heavy_minus_sign:                                                                                             | Permit category (e.g. solar, SOLAR, roofing, hvac — case insensitive)                                          |
| `status`                                                                                                       | [OptionalNullable[models.PermitStatus]](../../models/permitstatus.md)                                          | :heavy_minus_sign:                                                                                             | Permit status (e.g. issued, filed, final)                                                                      |
| `property_type`                                                                                                | [OptionalNullable[models.PropertyType]](../../models/propertytype.md)                                          | :heavy_minus_sign:                                                                                             | Property type (e.g. residential, commercial)                                                                   |
| `tag`                                                                                                          | *OptionalNullable[str]*                                                                                        | :heavy_minus_sign:                                                                                             | Filter by tag                                                                                                  |
| `record_kind`                                                                                                  | *Optional[str]*                                                                                                | :heavy_minus_sign:                                                                                             | Record kind: 'permit' (default, building permits only), 'contractor', 'tag', 'non_building', 'admin', or 'all' |
| `filed_after`                                                                                                  | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                   | :heavy_minus_sign:                                                                                             | Filed on or after this date                                                                                    |
| `filed_before`                                                                                                 | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                   | :heavy_minus_sign:                                                                                             | Filed on or before this date                                                                                   |
| `issued_after`                                                                                                 | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                   | :heavy_minus_sign:                                                                                             | Issued on or after this date                                                                                   |
| `issued_before`                                                                                                | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                   | :heavy_minus_sign:                                                                                             | Issued on or before this date                                                                                  |
| `min_value`                                                                                                    | *OptionalNullable[float]*                                                                                      | :heavy_minus_sign:                                                                                             | Minimum estimated value                                                                                        |
| `max_value`                                                                                                    | *OptionalNullable[float]*                                                                                      | :heavy_minus_sign:                                                                                             | Maximum estimated value                                                                                        |
| `q`                                                                                                            | *OptionalNullable[str]*                                                                                        | :heavy_minus_sign:                                                                                             | Full-text search query                                                                                         |
| `contractor_name`                                                                                              | *OptionalNullable[str]*                                                                                        | :heavy_minus_sign:                                                                                             | Contractor name (partial match)                                                                                |
| `page`                                                                                                         | *Optional[int]*                                                                                                | :heavy_minus_sign:                                                                                             | N/A                                                                                                            |
| `per_page`                                                                                                     | *Optional[int]*                                                                                                | :heavy_minus_sign:                                                                                             | N/A                                                                                                            |
| `retries`                                                                                                      | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                               | :heavy_minus_sign:                                                                                             | Configuration to override the default retry behavior of the client.                                            |

### Response

**[models.PermitSearchResponse](../../models/permitsearchresponse.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## export_permits

Export permits matching filters as CSV. Tier-gated row limits.

### Example Usage

<!-- UsageSnippet language="python" operationID="export_permits" method="get" path="/v1/permits/export" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.permits.export_permits(record_kind="permit", limit=1000)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                    | Type                                                                         | Required                                                                     | Description                                                                  |
| ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- | ---------------------------------------------------------------------------- |
| `zip_code`                                                                   | *OptionalNullable[str]*                                                      | :heavy_minus_sign:                                                           | N/A                                                                          |
| `city`                                                                       | *OptionalNullable[str]*                                                      | :heavy_minus_sign:                                                           | N/A                                                                          |
| `state`                                                                      | *OptionalNullable[str]*                                                      | :heavy_minus_sign:                                                           | N/A                                                                          |
| `category`                                                                   | *OptionalNullable[str]*                                                      | :heavy_minus_sign:                                                           | N/A                                                                          |
| `status`                                                                     | [OptionalNullable[models.PermitStatus]](../../models/permitstatus.md)        | :heavy_minus_sign:                                                           | N/A                                                                          |
| `property_type`                                                              | [OptionalNullable[models.PropertyType]](../../models/propertytype.md)        | :heavy_minus_sign:                                                           | N/A                                                                          |
| `tag`                                                                        | *OptionalNullable[str]*                                                      | :heavy_minus_sign:                                                           | N/A                                                                          |
| `record_kind`                                                                | *Optional[str]*                                                              | :heavy_minus_sign:                                                           | N/A                                                                          |
| `filed_after`                                                                | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects) | :heavy_minus_sign:                                                           | N/A                                                                          |
| `filed_before`                                                               | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects) | :heavy_minus_sign:                                                           | N/A                                                                          |
| `issued_after`                                                               | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects) | :heavy_minus_sign:                                                           | N/A                                                                          |
| `issued_before`                                                              | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects) | :heavy_minus_sign:                                                           | N/A                                                                          |
| `min_value`                                                                  | *OptionalNullable[float]*                                                    | :heavy_minus_sign:                                                           | N/A                                                                          |
| `max_value`                                                                  | *OptionalNullable[float]*                                                    | :heavy_minus_sign:                                                           | N/A                                                                          |
| `q`                                                                          | *OptionalNullable[str]*                                                      | :heavy_minus_sign:                                                           | N/A                                                                          |
| `contractor_name`                                                            | *OptionalNullable[str]*                                                      | :heavy_minus_sign:                                                           | N/A                                                                          |
| `limit`                                                                      | *Optional[int]*                                                              | :heavy_minus_sign:                                                           | N/A                                                                          |
| `retries`                                                                    | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)             | :heavy_minus_sign:                                                           | Configuration to override the default retry behavior of the client.          |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## get_permit

Get full details for a single permit.

### Example Usage

<!-- UsageSnippet language="python" operationID="get_permit" method="get" path="/v1/permits/{permit_id}" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.permits.get_permit(permit_id="8b0513b0-82c1-4220-9ede-cf81253853d0")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `permit_id`                                                         | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.PermitDetail](../../models/permitdetail.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## get_permits_by_address

Get all permits for a specific address (partial match).

### Example Usage

<!-- UsageSnippet language="python" operationID="get_permits_by_address" method="get" path="/v1/permits/address/{address}" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.permits.get_permits_by_address(address="5701 Alexanne Point", page=1, per_page=25)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `address`                                                           | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `page`                                                              | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `per_page`                                                          | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.PermitSearchResponse](../../models/permitsearchresponse.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## get_coverage_stats

Get coverage statistics — total permits, jurisdictions, and breakdown by city.

### Example Usage

<!-- UsageSnippet language="python" operationID="get_coverage_stats" method="get" path="/v1/permits/stats/coverage" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.permits.get_coverage_stats()

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