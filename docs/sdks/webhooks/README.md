# Webhooks

## Overview

New and changed permits pushed to your endpoint about 60 seconds after we ingest them; most sources are ingested nightly. Developer plan ($79/mo) and above.

### Available Operations

* [list_webhooks](#list_webhooks) - List Webhooks
* [create_webhook](#create_webhook) - Create Webhook
* [delete_webhook](#delete_webhook) - Delete Webhook
* [update_webhook](#update_webhook) - Update Webhook
* [test_webhook](#test_webhook) - Test Webhook
* [get_webhook_deliveries](#get_webhook_deliveries) - Get Webhook Deliveries
* [rotate_webhook_secret](#rotate_webhook_secret) - Rotate Webhook Secret
* [get_webhook_secret](#get_webhook_secret) - Get Webhook Secret

## list_webhooks

List all your registered webhooks.

### Example Usage

<!-- UsageSnippet language="python" operationID="list_webhooks" method="get" path="/v1/webhooks/" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.webhooks.list_webhooks()

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
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## create_webhook

Register a webhook to be notified when new permits match your filters.

Available on the Developer plan and above (see /v1/billing/plans for current
pricing). Maximum 10 webhooks per API key.
When a new permit matches your filters, we'll POST the permit data as JSON to your URL.
Set contractor_name to track a specific company — you'll get a POST within minutes
of any permit they pull appearing in our data (competitor tracking).

### Example Usage

<!-- UsageSnippet language="python" operationID="create_webhook" method="post" path="/v1/webhooks/" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.webhooks.create_webhook(url="https://helpful-cafe.biz")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                                                                                                                 | Type                                                                                                                                                      | Required                                                                                                                                                  | Description                                                                                                                                               |
| --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `url`                                                                                                                                                     | *str*                                                                                                                                                     | :heavy_check_mark:                                                                                                                                        | N/A                                                                                                                                                       |
| `city`                                                                                                                                                    | *OptionalNullable[str]*                                                                                                                                   | :heavy_minus_sign:                                                                                                                                        | N/A                                                                                                                                                       |
| `state`                                                                                                                                                   | *OptionalNullable[str]*                                                                                                                                   | :heavy_minus_sign:                                                                                                                                        | N/A                                                                                                                                                       |
| `category`                                                                                                                                                | *OptionalNullable[str]*                                                                                                                                   | :heavy_minus_sign:                                                                                                                                        | N/A                                                                                                                                                       |
| `zip_code`                                                                                                                                                | *OptionalNullable[str]*                                                                                                                                   | :heavy_minus_sign:                                                                                                                                        | N/A                                                                                                                                                       |
| `keyword`                                                                                                                                                 | *OptionalNullable[str]*                                                                                                                                   | :heavy_minus_sign:                                                                                                                                        | N/A                                                                                                                                                       |
| `contractor_name`                                                                                                                                         | *OptionalNullable[str]*                                                                                                                                   | :heavy_minus_sign:                                                                                                                                        | Fire only for permits pulled by contractors whose name contains this text (case-insensitive) — track a competitor or partner as their new permits arrive. |
| `retries`                                                                                                                                                 | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)                                                                                          | :heavy_minus_sign:                                                                                                                                        | Configuration to override the default retry behavior of the client.                                                                                       |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.FeatureLockedError      | 403                            | application/json               |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## delete_webhook

Delete a webhook.

### Example Usage

<!-- UsageSnippet language="python" operationID="delete_webhook" method="delete" path="/v1/webhooks/{webhook_id}" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.webhooks.delete_webhook(webhook_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `webhook_id`                                                        | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## update_webhook

Re-activate (or deactivate) one of your webhooks.

Re-activating resumes delivery from now: permits ingested while the webhook was paused
are not replayed (use /v1/permits/search or /v1/permits/sync to backfill a gap), so a
newly fixed endpoint is not hit with the whole backlog at once. The failure count resets
to zero.

### Example Usage

<!-- UsageSnippet language="python" operationID="update_webhook" method="patch" path="/v1/webhooks/{webhook_id}" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.webhooks.update_webhook(webhook_id="<id>", is_active=True)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `webhook_id`                                                        | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `is_active`                                                         | *bool*                                                              | :heavy_check_mark:                                                  | true re-activates a webhook the failure breaker switched off.       |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## test_webhook

Send a test event to a webhook URL.

Useful for verifying your webhook endpoint is reachable and signature 
validation works. Sends a fake permit payload with event=permit.test.

### Example Usage

<!-- UsageSnippet language="python" operationID="test_webhook" method="post" path="/v1/webhooks/{webhook_id}/test" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.webhooks.test_webhook(webhook_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `webhook_id`                                                        | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## get_webhook_deliveries

Why your webhook is or is not being delivered, seen from our side of the connection.

Only FAILED attempts are recorded individually; successful deliveries are counted
(fire_count, last_fired_at). An empty `recent_failures` list is therefore good news, not
missing data. `consecutive_failures` is what the automatic pause acts on: when it reaches
the limit the webhook is deactivated, so it is the field to watch.

### Example Usage

<!-- UsageSnippet language="python" operationID="get_webhook_deliveries" method="get" path="/v1/webhooks/{webhook_id}/deliveries" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.webhooks.get_webhook_deliveries(webhook_id="<id>", limit=20)

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `webhook_id`                                                        | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `limit`                                                             | *Optional[int]*                                                     | :heavy_minus_sign:                                                  | How many recent failed attempts to return.                          |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## rotate_webhook_secret

Issue a NEW signing secret for this webhook. The old one stops working immediately.

Every delivery after this call is signed with the new secret, so update your verifier
first. Creating a webhook again with the same settings returns the existing secret; this
endpoint is the only way to rotate it.

### Example Usage

<!-- UsageSnippet language="python" operationID="rotate_webhook_secret" method="post" path="/v1/webhooks/{webhook_id}/rotate-secret" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.webhooks.rotate_webhook_secret(webhook_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `webhook_id`                                                        | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## get_webhook_secret

Retrieve your webhook signing secret. Use this to validate signatures.

The X-PermitStack-Signature header on incoming webhook requests is the
HMAC-SHA256 of the request body using this secret. Verify before 
processing to ensure the request came from PermitStack.

### Example Usage

<!-- UsageSnippet language="python" operationID="get_webhook_secret" method="get" path="/v1/webhooks/{webhook_id}/secret" -->
```python
import os
from permitstack import Permitstack


with Permitstack(
    api_key=os.getenv("PERMITSTACK_API_KEY", ""),
) as p_client:

    res = p_client.webhooks.get_webhook_secret(webhook_id="<id>")

    # Handle response
    print(res)

```

### Parameters

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `webhook_id`                                                        | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
| errors.ErrorDetail             | 401, 429                       | application/json               |
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |