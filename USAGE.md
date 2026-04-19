<!-- Start SDK Example Usage [usage] -->
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