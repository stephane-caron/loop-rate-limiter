# Loop rate limiters

[![Build](https://img.shields.io/github/workflow/status/stephane-caron/loop-rate-limiters/CI)](https://github.com/stephane-caron/loop-rate-limier/actions)
[![Coverage](https://coveralls.io/repos/github/stephane-caron/loop-rate-limiters/badge.svg?branch=main)](https://coveralls.io/github/stephane-caron/loop-rate-limiters?branch=main)
[![PyPI version](https://img.shields.io/pypi/v/loop-rate-limiters)](https://pypi.org/project/loop-rate-limiters/)

Simple loop frequency regulators in Python with an API similar to [``rospy.Rate``](https://wiki.ros.org/rospy/Overview/Time#Sleeping_and_Rates).

## Installation

```sh
pip install loop-rate-limiters
```

## Usage

The ``RateLimiter`` class provides a loop frequency limiter:

```python
from loop_rate_limiters import RateLimiter
from time import perf_counter

rate = RateLimiter(frequency=400.0)
while True:
    print(f"Hello from loop at {perf_counter():.3f} s")
    rate.sleep()
```

### asyncio

The ``AsyncRateLimiter`` class provides a loop frequency limiter for asyncio:

```python
import asyncio
from loop_rate_limiters import AsyncRateLimiter

async def main():
    rate = AsyncRateLimiter(frequency=400.0)
    while True:
        loop_time = asyncio.get_event_loop().time()
        print(f"Hello from loop at {loop_time:.3f} s")
        await rate.sleep()

if __name__ == "__main__":
    asyncio.run(main())
```
