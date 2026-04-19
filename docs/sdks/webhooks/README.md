# Webhooks

## Overview

Subscribe to real-time permit events (paid tiers)

### Available Operations

* [list_webhooks](#list_webhooks) - List Webhooks
* [create_webhook](#create_webhook) - Create Webhook
* [delete_webhook](#delete_webhook) - Delete Webhook

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
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |

## create_webhook

Register a webhook to be notified when new permits match your filters.

Available on Starter ($49/mo) and above. Maximum 10 webhooks per API key.
When a new permit matches your filters, we'll POST the permit data as JSON to your URL.

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

| Parameter                                                           | Type                                                                | Required                                                            | Description                                                         |
| ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- | ------------------------------------------------------------------- |
| `url`                                                               | *str*                                                               | :heavy_check_mark:                                                  | N/A                                                                 |
| `city`                                                              | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | N/A                                                                 |
| `state`                                                             | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | N/A                                                                 |
| `category`                                                          | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | N/A                                                                 |
| `zip_code`                                                          | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | N/A                                                                 |
| `description`                                                       | *OptionalNullable[str]*                                             | :heavy_minus_sign:                                                  | N/A                                                                 |
| `retries`                                                           | [Optional[utils.RetryConfig]](../../models/utils/retryconfig.md)    | :heavy_minus_sign:                                                  | Configuration to override the default retry behavior of the client. |

### Response

**[Any](../../models/.md)**

### Errors

| Error Type                     | Status Code                    | Content Type                   |
| ------------------------------ | ------------------------------ | ------------------------------ |
| errors.HTTPValidationError     | 422                            | application/json               |
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
| errors.PermitstackDefaultError | 4XX, 5XX                       | \*/\*                          |