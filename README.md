# Russia Twitter Throttle Dataset

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)

This is a dataset of a measurements collected from <https://lynx.pink/is-my-twitter-slow-or-what>

## License and required attribution

This dataset is licensed under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). This permits anyone to copy, redistribute, remix, transmit and adapt the work provided the original work and source is appropriately cited.

Citation example (markdown):

```markdown
"[Russia Twitter Throttle Dataset](https://github.com/4ndv/russia-twitter-throttle)" by [Andrey Viktorov](https://lynx.pink) and [Leonid Evdokimov](https://darkk.net.ru) is licensed under a [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/).
```

Parts of this dataset contains information, gathered from CAIDA UCSD datasets, which also requires attribution:

```text
The CAIDA UCSD [DataSet Name] - [dates used],
https://www.caida.org/data/[dataset-URL]
```

The used datasets are:

- [Routeviews Prefix to AS mappings Dataset (pfx2as) for IPv4 and IPv6](https://www.caida.org/catalog/datasets/routeviews-prefix2as/)
- [Inferred AS to Organization Mapping Dataset](https://www.caida.org/catalog/datasets/as-organizations/)

## Data structure

For each month there is a folder in `data/`, in the format of `YYYY-MM`. Each folder contains a separate csv file for each day of the month (for example, `data/2021-04/01.csv` is an April 1st, 2021) with such fields:

`datetime_rounded` - measurement timestamp in UTC, rounded down to the 5-minute intervals

`anonymized_ip` - IP address of the measuring user. For ipv4 there is a last octet stripped, for ipv6 there is last 80 bits stripped (done via `ip_anonymizer` ruby gem)

`subnet` - IP subnet, gathered from CAIDA UCSD dataset

`asn` - Autonomous System Number, gathered from CAIDA UCSD dataset

`as_country` - AS Country, gathered from CAIDA UCSD dataset

`as_organization` - AS Organization Name, gathered from CAIDA UCSD dataset

`as_organization_iden` - AS Organization identifier, gathered from CAIDA UCSD dataset

`version` - Measurement version, which differs by servers used for "control" and "control taco" test results.

`test_result` - Download speed in kbps from `abs.twimg.com`

`control_result` - Download speed in kbps from a control non-throttled server, to filter out any users with the slow internet connection

`control_taco_result` - Download speed in kbps from a control server, which domain contains `t.co` part. For some time RKN in Russia throttled all the domains which contained `t.co` at some place, like githubuserconten**t.co**m

Rows are ordered by `datetime_rounded ASC, anonymized_ip ASC, test_result ASC`

Fell free to ask any questions via Github Issues!
