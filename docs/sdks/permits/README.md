# Permits

## Overview

Search and retrieve building permits

### Available Operations

* [search_permits](#search_permits) - Search Permits
* [export_permits](#export_permits) - Export Permits
* [list_permit_events](#list_permit_events) - List Permit Events
* [get_permit](#get_permit) - Get Permit
* [get_permits_by_address](#get_permits_by_address) - Get Permits By Address
* [get_coverage_stats](#get_coverage_stats) - Get Coverage Stats
* [list_plays](#list_plays) - List Plays
* [battery_retrofit_candidates](#battery_retrofit_candidates) - Battery Retrofit Candidates
* [orphan_recovery](#orphan_recovery) - Orphan Recovery

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

| Parameter                                                                                                                                                                                        | Type                                                                                                                                                                                             | Required                                                                                                                                                                                         | Description                                                                                                                                                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `zip_code`                                                                                                                                                                                       | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | 5-digit ZIP code                                                                                                                                                                                 |
| `city`                                                                                                                                                                                           | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | City name                                                                                                                                                                                        |
| `state`                                                                                                                                                                                          | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | 2-letter state code                                                                                                                                                                              |
| `jurisdiction`                                                                                                                                                                                   | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | Jurisdiction name (e.g. 'Wake County', 'Tacoma') or partial match                                                                                                                                |
| `address`                                                                                                                                                                                        | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | Street address, partial + case-insensitive (e.g. '1600 Pennsylvania') — indexed, fast                                                                                                            |
| `lat`                                                                                                                                                                                            | *OptionalNullable[float]*                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                               | Latitude for radius search                                                                                                                                                                       |
| `lng`                                                                                                                                                                                            | *OptionalNullable[float]*                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                               | Longitude for radius search                                                                                                                                                                      |
| `radius_miles`                                                                                                                                                                                   | *Optional[float]*                                                                                                                                                                                | :heavy_minus_sign:                                                                                                                                                                               | Radius in miles (used with lat/lng)                                                                                                                                                              |
| `bbox`                                                                                                                                                                                           | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | Map-viewport bounding box 'minLng,minLat,maxLng,maxLat'. Returns permits whose location falls inside the box (geocoded permits only).                                                            |
| `polygon`                                                                                                                                                                                        | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | A drawn area as a GeoJSON Polygon geometry (URL-encoded), e.g. {"type":"Polygon","coordinates":[[[lng,lat],...]]}. Returns permits inside the polygon (geocoded permits only).                   |
| `category`                                                                                                                                                                                       | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | Permit category (e.g. solar, SOLAR, roofing, hvac — case insensitive)                                                                                                                            |
| `status`                                                                                                                                                                                         | [OptionalNullable[models.PermitStatus]](../../models/permitstatus.md)                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                               | Permit status (e.g. issued, filed, final)                                                                                                                                                        |
| `property_type`                                                                                                                                                                                  | [OptionalNullable[models.PropertyType]](../../models/propertytype.md)                                                                                                                            | :heavy_minus_sign:                                                                                                                                                                               | Property type (e.g. residential, commercial)                                                                                                                                                     |
| `tag`                                                                                                                                                                                            | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | Filter by tag                                                                                                                                                                                    |
| `record_kind`                                                                                                                                                                                    | *Optional[str]*                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                               | Record kind: 'permit' (default, building permits only), 'contractor', 'tag', 'non_building', 'admin', or 'all'                                                                                   |
| `filed_after`                                                                                                                                                                                    | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                               | Filed on or after this date                                                                                                                                                                      |
| `filed_before`                                                                                                                                                                                   | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                               | Filed on or before this date                                                                                                                                                                     |
| `issued_after`                                                                                                                                                                                   | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                               | Issued on or after this date                                                                                                                                                                     |
| `issued_before`                                                                                                                                                                                  | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                               | Issued on or before this date                                                                                                                                                                    |
| `date_after`                                                                                                                                                                                     | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                               | On or after this date, matched against whichever date a record has (issued, else filed). Use this when a source populates only one of issued/filed — e.g. issued-only feeds vs filed-only feeds. |
| `date_before`                                                                                                                                                                                    | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)                                                                                                                     | :heavy_minus_sign:                                                                                                                                                                               | On or before this date, matched against whichever date a record has (issued, else filed).                                                                                                        |
| `parcel`                                                                                                                                                                                         | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | Parcel number / APN / folio (formatting ignored). Returns permits on that parcel where the source publishes one.                                                                                 |
| `min_value`                                                                                                                                                                                      | *OptionalNullable[float]*                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                               | Minimum estimated value                                                                                                                                                                          |
| `max_value`                                                                                                                                                                                      | *OptionalNullable[float]*                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                               | Maximum estimated value                                                                                                                                                                          |
| `min_solar_kw`                                                                                                                                                                                   | *OptionalNullable[float]*                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                               | Minimum extracted solar system size (kW DC)                                                                                                                                                      |
| `max_solar_kw`                                                                                                                                                                                   | *OptionalNullable[float]*                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                               | Maximum extracted solar system size (kW DC)                                                                                                                                                      |
| `min_sqft`                                                                                                                                                                                       | *OptionalNullable[float]*                                                                                                                                                                        | :heavy_minus_sign:                                                                                                                                                                               | Minimum square footage mentioned (from enrichment)                                                                                                                                               |
| `has_enrichment`                                                                                                                                                                                 | *OptionalNullable[bool]*                                                                                                                                                                         | :heavy_minus_sign:                                                                                                                                                                               | Only permits that have (true) or lack (false) LLM enrichment                                                                                                                                     |
| `scope`                                                                                                                                                                                          | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | Substring match on the enriched work scope                                                                                                                                                       |
| `q`                                                                                                                                                                                              | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | Case-insensitive substring match across description, address, and permit number                                                                                                                  |
| `contractor_name`                                                                                                                                                                                | *OptionalNullable[str]*                                                                                                                                                                          | :heavy_minus_sign:                                                                                                                                                                               | Contractor name (partial match)                                                                                                                                                                  |
| `page`                                                                                                                                                                                           | *Optional[int]*                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                               | N/A                                                                                                                                                                                              |
| `per_page`                                                                                                                                                                                       | *Optional[int]*                                                                                                                                                                                  | :heavy_minus_sign:                                                                                                                                                                               | N/A                                                                                                                                                                                              |
| `retries`                                                                                                                                                                                        | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                                                                 | :heavy_minus_sign:                                                                                                                                                                               | Configuration to override the default retry behavior of the client.                                                                                                                              |

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

| Parameter                                                                                 | Type                                                                                      | Required                                                                                  | Description                                                                               |
| ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------- |
| `zip_code`                                                                                | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `city`                                                                                    | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `state`                                                                                   | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `category`                                                                                | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `status`                                                                                  | [OptionalNullable[models.PermitStatus]](../../models/permitstatus.md)                     | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `property_type`                                                                           | [OptionalNullable[models.PropertyType]](../../models/propertytype.md)                     | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `tag`                                                                                     | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `record_kind`                                                                             | *Optional[str]*                                                                           | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `filed_after`                                                                             | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)              | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `filed_before`                                                                            | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)              | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `issued_after`                                                                            | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)              | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `issued_before`                                                                           | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)              | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `date_after`                                                                              | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)              | :heavy_minus_sign:                                                                        | On or after this date, matched against whichever date a record has (issued, else filed).  |
| `date_before`                                                                             | [datetime](https://docs.python.org/3/library/datetime.html#datetime-objects)              | :heavy_minus_sign:                                                                        | On or before this date, matched against whichever date a record has (issued, else filed). |
| `parcel`                                                                                  | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | Parcel number / APN / folio (formatting ignored).                                         |
| `min_value`                                                                               | *OptionalNullable[float]*                                                                 | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `max_value`                                                                               | *OptionalNullable[float]*                                                                 | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `min_solar_kw`                                                                            | *OptionalNullable[float]*                                                                 | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `max_solar_kw`                                                                            | *OptionalNullable[float]*                                                                 | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `min_sqft`                                                                                | *OptionalNullable[float]*                                                                 | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `has_enrichment`                                                                          | *OptionalNullable[bool]*                                                                  | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `scope`                                                                                   | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `q`                                                                                       | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `contractor_name`                                                                         | *OptionalNullable[str]*                                                                   | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `limit`                                                                                   | *Optional[int]*                                                                           | :heavy_minus_sign:                                                                        | N/A                                                                                       |
| `retries`                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                          | :heavy_minus_sign:                                                                        | Configuration to override the default retry behavior of the client.                       |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## list_permit_events

Queryable feed of permit status/date transitions (new_permit, status_change,
issued, completed, expired), built from a daily-ingest diff. A real-time,
historical, filter-scoped change feed no competitor offers below enterprise —
pair it with a webhook to be alerted the moment a matching permit changes status.

### Example Usage

<!-- UsageSnippet language="python" operationID="list_permit_events" method="get" path="/v1/permits/events" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.permits.list_permit_events(page=1, per_page=50)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                   | Type                                                                        | Required                                                                    | Description                                                                 |
| --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- | --------------------------------------------------------------------------- |
| `event_type`                                                                | *OptionalNullable[str]*                                                     | :heavy_minus_sign:                                                          | Filter by event type: new_permit, status_change, issued, completed, expired |
| `category`                                                                  | *OptionalNullable[str]*                                                     | :heavy_minus_sign:                                                          | Permit category (e.g. solar, battery)                                       |
| `city`                                                                      | *OptionalNullable[str]*                                                     | :heavy_minus_sign:                                                          | City name                                                                   |
| `state`                                                                     | *OptionalNullable[str]*                                                     | :heavy_minus_sign:                                                          | 2-letter state code                                                         |
| `jurisdiction`                                                              | *OptionalNullable[str]*                                                     | :heavy_minus_sign:                                                          | Jurisdiction name (partial)                                                 |
| `permit_id`                                                                 | *OptionalNullable[str]*                                                     | :heavy_minus_sign:                                                          | Events for a single permit id                                               |
| `detected_after`                                                            | [date](https://docs.python.org/3/library/datetime.html#date-objects)        | :heavy_minus_sign:                                                          | Only events detected on/after this UTC timestamp (ISO 8601)                 |
| `page`                                                                      | *Optional[int]*                                                             | :heavy_minus_sign:                                                          | N/A                                                                         |
| `per_page`                                                                  | *Optional[int]*                                                             | :heavy_minus_sign:                                                          | N/A                                                                         |
| `retries`                                                                   | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)            | :heavy_minus_sign:                                                          | Configuration to override the default retry behavior of the client.         |

### Response

**[models.PermitEventsResponse](../../models/permiteventsresponse.md)**

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

## list_plays

List available trade plays and their parameters.

### Example Usage

<!-- UsageSnippet language="python" operationID="list_plays" method="get" path="/v1/plays" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.permits.list_plays()

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

## battery_retrofit_candidates

Solar permits aged between min/max years whose address has NO battery permit
on file — the storage-retrofit lead list. Requires a location filter.

### Example Usage

<!-- UsageSnippet language="python" operationID="battery_retrofit_candidates" method="get" path="/v1/plays/battery-retrofit-candidates" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.permits.battery_retrofit_candidates(min_age_years=2, max_age_years=7, page=1, per_page=25)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `state`                                                             | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | 2-letter state code                                                 |
| `city`                                                              | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | City name                                                           |
| `zip_code`                                                          | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | 5-digit ZIP                                                         |
| `jurisdiction`                                                      | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | Jurisdiction name (partial)                                         |
| `min_age_years`                                                     | *Optional[float]*                                                   | :heavy_minus_sign:                                                  | Minimum age of the PV permit, in years                              |
| `max_age_years`                                                     | *Optional[float]*                                                   | :heavy_minus_sign:                                                  | Maximum age of the PV permit, in years                              |
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

## orphan_recovery

PV permits whose installer (contractor, applicant, or owner) matches `installer`
in a territory — a named competitor's customer base. Requires a location filter.

### Example Usage

<!-- UsageSnippet language="python" operationID="orphan_recovery" method="get" path="/v1/plays/orphan-recovery" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.permits.orphan_recovery(installer="<value>", page=1, per_page=25)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `installer`                                                         | *str*                                                               | :heavy_check_mark:                                                  | Installer name to match (contractor/applicant/owner)                |
| `state`                                                             | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | 2-letter state code                                                 |
| `city`                                                              | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | City name                                                           |
| `zip_code`                                                          | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | 5-digit ZIP                                                         |
| `jurisdiction`                                                      | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | Jurisdiction name (partial)                                         |
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