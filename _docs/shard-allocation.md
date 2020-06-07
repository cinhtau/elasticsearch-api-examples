---
title: Shard Allocation
description: Move shards between Nodes
---

## Cluster Settings

Check cluster settings (output is yaml format)
```
GET _cluster/settings?format=yaml
```

yaml output
```yaml
persistent:
  cluster:
    routing:
      allocation:
        enable: "all"
transient:
  cluster:
    routing:
      allocation:
        disk:
          watermark:
            low: "85%"
            high: "60gb"
        enable: "all"
        exclude:
          _ip: ""
    info:
      update:
        interval: "1m"
  logger:
    action:
      level: "WARN"
```

## Enable Shard Allocation

```bash
curl -XPUT "http://vip-fo-test-es:9200/_cluster/settings" -H 'Content-Type: application/json' -d'
{
    "transient" : {
        "cluster.routing.allocation.enable" : "all"
    }
}'
```

## Disable Shard Allocation

```bash
curl -XPUT "http://vip-fo-test-es:9200/_cluster/settings" -H 'Content-Type: application/json' -d'
{
    "transient" : {
        "cluster.routing.allocation.enable" : "none"
    }
}'
```


### Disable shard allocation on a node

```
PUT /_cluster/settings
{
  "transient" : {
    "cluster.routing.allocation.exclude._ip" : "10.22.63.221"
  }
}
```

### Reset setting

```

PUT /_cluster/settings
{
  "transient" : {
    "cluster.routing.allocation.exclude._ip" : ""
  }
}
```
