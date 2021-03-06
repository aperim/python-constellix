# Python Library for Constellix API

![PyPI](https://github.com/aperim/python-constellix/workflows/Publish%20Python%20%F0%9F%90%8D%20distributions%20%F0%9F%93%A6%20to%20PyPI%20and%20TestPyPI/badge.svg?branch=main) [![GitHub issues](https://img.shields.io/github/issues/aperim/python-constellix?style=plastic)](https://github.com/aperim/python-constellix/issues) [![GitHub forks](https://img.shields.io/github/forks/aperim/python-constellix?style=plastic)](https://github.com/aperim/python-constellix/network) [![GitHub stars](https://img.shields.io/github/stars/aperim/python-constellix?style=plastic)](https://github.com/aperim/python-constellix/stargazers) [![GitHub license](https://img.shields.io/github/license/aperim/python-constellix?style=plastic)](https://github.com/aperim/python-constellix/blob/main/LICENSE.txt) [![Twitter](https://img.shields.io/twitter/url?style=social&url=https%3A%2F%2Fgithub.com%2Faperim%2Fpython-constellix)](https://twitter.com/intent/tweet?url=https%3A%2F%2Fgithub.com%2Faperim%2Fpython-constellix&via=troykelly&text=Access%20the%20Constellix%20DNS%20API%20From%20Python&hashtags=%23python%20%23devops%20%23dns%20%23api)

## Description

Connects to the [Constellix API](https://api-docs.constellix.com/) and does things

### Note

This is in no way affiliated with Constellix.

### Issues

The tokens generated by this library are rejected about 50% of the time.
The library uses `backoff` to manage these failures and typically takes less than 20 retries per payload to get the response you want.

### Logging / Debugging

This library uses `logging` just set the log level and format you need.

## Example

### Set up environment

```bash
export CONSTELLIX_APISECRET=48d4ebb7-246e-406a-b272-2e174a3bdf35
export CONSTELLIX_APIKEY=b6f11837-9858-4f7f-8b3f-50057355e8e9
```

### List all domains in account

```python
from constellix import Constellix
import asyncio

api_key = os.environ.get("CONSTELLIX_APIKEY")
secret_key = os.environ.get("CONSTELLIX_APISECRET")

async def list_all_domains(api):
	domains = await api.domains.all()
	print(domains)

loop = asyncio.get_event_loop()
api = Constellix(api_key=api_key, secret_key=secret_key, loop=loop)
loop.run_until_complete(list_all_domains(api))
```

### Search for a domain

```python
domains = await api.domains.search("example")
```

```python
domains = await api.domains.search_startswith("example")
```

```python
domains = await api.domains.search_endswith("com")
```

```python
domains = await api.domains.search_exact("example.com")
```

### Create a new domain

```python
domain = await api.domains.create("example.com")
```

#### And then delete it

```python
delete_success = await domain.delete()
```

### Get all a domains records

```python
all_records = await domain.records.all()
```

## Support

<a href="https://www.buymeacoffee.com/troykelly" target="_blank"><img src="https://cdn.buymeacoffee.com/buttons/v2/default-yellow.png" alt="Buy Me A Coffee" style="height: 60px !important;width: 217px !important;" ></a>
