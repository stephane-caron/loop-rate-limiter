# Loop rate limiters

[![Build](https://img.shields.io/github/actions/workflow/status/upkie/loop-rate-limiters/main.yml?branch=main)](https://github.com/upkie/loop-rate-limiters/actions)
[![Documentation](https://img.shields.io/github/actions/workflow/status/upkie/loop-rate-limiters/docs.yml?branch=main&label=docs)](https://upkie.github.io/loop-rate-limiters/)
[![Coverage](https://coveralls.io/repos/github/upkie/loop-rate-limiters/badge.svg?branch=main)](https://coveralls.io/github/upkie/loop-rate-limiters?branch=main)
[![Conda version](https://img.shields.io/conda/vn/conda-forge/loop-rate-limiters.svg)](https://anaconda.org/conda-forge/loop-rate-limiters)
[![PyPI version](https://img.shields.io/pypi/v/loop-rate-limiters)](https://pypi.org/project/loop-rate-limiters/)

Simple loop frequency regulators in Python with an API similar to ``rospy.Rate``:

```python
from loop_rate_limiters import RateLimiter
from time import perf_counter

rate = RateLimiter(frequency=400.0)
while True:
    print(f"Hello from loop at {perf_counter():.3f} s")
    rate.sleep()
```

A similar ``AsyncRateLimiter`` class is available for [asynchronous code](https://github.com/upkie/loop-rate-limiters#asynchronous-io).

## Installation

### From conda-forge

```console
conda install -c conda-forge loop-rate-limiters
```

### From PyPI

```console
pip install loop-rate-limiters
```

## Asynchronous I/O

The ``AsyncRateLimiter`` class provides a loop frequency limiter for [asyncio](https://docs.python.org/3/library/asyncio.html):

```python
import asyncio
from loop_rate_limiters import AsyncRateLimiter

async def main():
    rate = AsyncRateLimiter(frequency=400.0)
    while True:
        loop_time = asyncio.get_event_loop().time()
        print(f"Hello from loop at {loop_time:.3f} s")
        await rate.sleep()

asyncio.run(main())
```

This can be used if, for instance, there are several tasks executed in parallel at different frequencies.

## See also

- [ischedule](https://github.com/aleksve/ischedule): single-thread interval scheduler in Python
