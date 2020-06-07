Back to [Main](README.md)

## Catalog

Get verbose output
```http
GET _cat/indices?v
```

Output
```text
health status index                         uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   metrics-2017.02.08            2LjFJYDrSlifpNRTGfQODg   2   1    6715909            0      3.3gb          1.7gb
```

## Check master nodes

Kibana Console
```text
GET _cat/master?v
```

Example Output
```text
id                     host         ip           node
mu7on18lTkCsuI2EeY1X0Q mtzhlrshld03 10.22.63.221 Setinal Rock
```
## Sorting on fields

Get closed indices first
```http
GET /_cat/indices?v&s=status:asc
```

Get biggest indices
```http
GET /_cat/indices?v&s=store.size:desc
```

Output
```text
health status index                         uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   ep2-itu-2017.02.08            QQ2b6T5dTr6hOYitNhhEWw   1   1   51843464            0     46.5gb         22.2gb
green  open   ep2-itu-2017.02.07            4nRKYhSRRDqRGMAVOZfDMg   1   1   23538256     21202000     35.5gb         17.7gb
green  open   ep2-itu-2017.02.06            7py8fEL7Qci3bsTmUvMsxA   1   1   16666008            0     11.7gb          5.8gb
```

Get index by name (year), e.g. indices about crime.

```text
GET _cat/indices/crimes-*?v&s=docs.count:desc

health status index       uuid                   pri rep docs.count docs.deleted store.size pri.store.size
green  open   crimes-2004 p2JCJniGT4eHDdv64kgZpA   1   0      45850         3434     18.4mb         18.4mb
green  open   crimes-2003 NKITCJsNRD6e9PkOulxGbQ   1   0      45504         3053     18.3mb         18.3mb
green  open   crimes-2005 TfkNQc89Rq6Ewa2nJ7-9XA   1   0      41244         3411     16.9mb         16.9mb
green  open   crimes-2006 ygNyLnHgRcyTomc3GAkGBA   1   0      38333         3979     15.8mb         15.8mb
green  open   crimes-2016 AoTIv6QfRDCQifW4xvDKnw   1   0      34979         2808     14.2mb         14.2mb
green  open   crimes-2007 K_cux2BYTROwZqsX8o83hg   1   0      33631         4054     13.8mb         13.8mb
green  open   crimes-2008 iARXGS8AS_quaZbaZBFK6Q   1   0      31552         3848     13.1mb         13.1mb
green  open   crimes-2015 tYPTl-WCTpmqNsyMSymaLQ   1   0      31490         2829     12.9mb         12.9mb
green  open   crimes-2014 TrNbfqs-SOy6C8W7l2_ypw   1   0      29863         2786     12.2mb         12.2mb
green  open   crimes-2009 YzJpXxE_QC-JHo_LH5Rx3g   1   0      28656         3531       12mb           12mb
green  open   crimes-2010 N80-1A9BTiSD40ZLE2KhaQ   1   0      26315         3366     10.9mb         10.9mb
green  open   crimes-2012 MkFc_NZbRhmR-NyvTOUsaA   1   0      25806         3426     10.6mb         10.6mb
green  open   crimes-2013 GDDaORknSDKNhcSGFW9aWQ   1   0      25755         3295     10.7mb         10.7mb
green  open   crimes-2011 737oWFgpQ8uJKG6UEd1xrg   1   0      25060         3500     10.5mb         10.5mb
green  open   crimes-2017 VM7g6AZtRh-z7tzSzlZuWA   1   0      16435         1393      6.8mb          6.8mb
green  open   crimes-2018 BJh7oXZDQee7V1JhoPvOSQ   1   0         45            0     37.2kb         37.2kb
green  open   crimes-2002 r4qGw78-TmSTISGjAIbjIQ   1   0         21            5     24.2kb         24.2kb
```

## Select Headers

If you need only specific values, you can use the header option to select for instance only the index name.

```http
GET _cat/indices/fo-log-2017*?h=index&s=index:asc

fo-log-2017.05.25
fo-log-2017.05.26
fo-log-2017.05.27
```

## Check Mapping

Check Mapping
```http
GET index_name/_mapping
```

Check Field Mapping
```http
GET index_name/_mapping/field/field_name
```
