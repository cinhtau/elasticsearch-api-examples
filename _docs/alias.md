---
title: Alias
description: Assign indices to an alias
---
[Current doc](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-aliases.html)

## Remove Indes from Alias

```json
POST /_aliases?pretty
{
  "actions": [
    {
      "remove": {
        "index": "proxy-utm-2020.06.03",
        "alias": "proxy-logs"
      }
    }
  ]
}
```
