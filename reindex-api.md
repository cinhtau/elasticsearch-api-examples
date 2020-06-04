# Reindex Data

Reindex without waiting for completion
```
POST /_reindex?wait_for_completion=false
{
  "source": {
    "index": "logs-2020.06.03"
  },
  "dest": {
    "index": "logs-fix-2020.06.03"
  }
}
```

List reindex tasks
```
GET /_tasks/?pretty&detailed=true&actions=*reindex
```

See also this [blog article](https://cinhtau.net/2016/09/19/reindex-data-in-elasticsearch/).
