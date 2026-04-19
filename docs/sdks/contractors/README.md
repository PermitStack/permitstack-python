# Contractors

## Overview

Search contractors and see their permit history

### Available Operations

* [search_contractors](#search_contractors) - Search Contractors
* [get_contractor](#get_contractor) - Get Contractor
* [get_contractor_permits](#get_contractor_permits) - Get Contractor Permits

## search_contractors

Search contractors by name, location, or specialty.

### Example Usage

<!-- UsageSnippet language="python" operationID="search_contractors" method="get" path="/v1/contractors/search" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.contractors.search_contractors(page=1, per_page=25)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `name`                                                              | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | Contractor name (partial match)                                     |
| `state`                                                             | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | 2-letter state code                                                 |
| `city`                                                              | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | City name                                                           |
| `specialty`                                                         | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | Specialty tag (e.g. solar, roofing, hvac)                           |
| `min_permits`                                                       | *OptionalNullable[int]*                                             | :heavy_minus_sign:                                                  | Minimum total permits                                               |
| `page`                                                              | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `per_page`                                                          | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ContractorSearchResponse](../../models/contractorsearchresponse.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## get_contractor

Get a contractor's full profile with permit stats.

### Example Usage

<!-- UsageSnippet language="python" operationID="get_contractor" method="get" path="/v1/contractors/{contractor_id}" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.contractors.get_contractor(contractor_id="d886f7c0-9af0-429f-a2d4-dfe6f2f526ae")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `contractor_id`                                                     | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[models.ContractorProfile](../../models/contractorprofile.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## get_contractor_permits

Get all permits associated with a contractor.

### Example Usage

<!-- UsageSnippet language="python" operationID="get_contractor_permits" method="get" path="/v1/contractors/{contractor_id}/permits" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.contractors.get_contractor_permits(contractor_id="a9c0dbb7-1080-46cd-85f9-7abfb02d5914", page=1, per_page=25)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `contractor_id`                                                     | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `page`                                                              | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `per_page`                                                          | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |