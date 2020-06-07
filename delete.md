Back to [Main](README.md)

# Delete Data

There a various ways to delete data in Elasticsearch.

## Delete Index

This will delete the whole index. Replace myindex with the index name.

```http
DELETE myindex
```

## Delete Documents within an Index

If you need to delete documents within an index use the delete by query API.

### Find Documents for Delete

First, find the documents you want to delete by a simple discriminator or complex condition. I prefer the first one. One example:

```bash
curl -XGET "http://elasticsearch:9200/fo-log-2017.07.11/_search" -H 'Content-Type: application/json' -d'
{
  "query": {
    "bool": {
      "must": [
        {
          "match": {
            "recordVersion": {
              "query": "74.0",
              "type": "phrase"
            }
          }
        }
      ]
    }
  }
}'
```

### Delete By Query
If the search lists the documents you want to delete you can use the query for delete.

```bash
curl -XPOST "http://elasticsearch:9200/fo-log-2017.07.11/_delete_by_query" -H 'Content-Type: application/json' -d'
{
   "query": {
    "bool": {
      "must": [
        {
          "match": {
            "recordVersion": {
              "query": "74.0",
              "type": "phrase"
            }
          }
        }
      ]
    }
  }
}'
```

### Check Task Status

This may be a long running task. You can always check with the Task API the current status.

The console template
```http
GET _tasks?detailed=true&actions=*/delete/byquery
```

The curl template
```bash
curl -XGET "http://elasticsearch:9200/_tasks?detailed=true&actions=*/delete/byquery"
```

The task output
```json
{
  "nodes": {
    "10wnM9s6QOm5Ye6pVgBXHg": {
      "name": "kibana-lb",
      "transport_address": "10.22.11.33:9300",
      "host": "elasticsearch",
      "ip": "10.22.11.33:9300",
      "roles": [],
      "attributes": {
        "rack": "with-nas",
        "ml.enabled": "true"
      },
      "tasks": {
        "10wnM9s6QOm5Ye6pVgBXHg:23539458": {
          "node": "10wnM9s6QOm5Ye6pVgBXHg",
          "id": 23539458,
          "type": "transport",
          "action": "indices:data/write/delete/byquery",
          "status": {
            "total": 424578,
            "updated": 0,
            "created": 0,
            "deleted": 291000,
            "batches": 291,
            "version_conflicts": 0,
            "noops": 0,
            "retries": {
              "bulk": 0,
              "search": 0
            },
            "throttled_millis": 0,
            "requests_per_second": -1,
            "throttled_until_millis": 0
          },
          "description": "delete-by-query [fo-log-2017.07.11]",
          "start_time_in_millis": 1499765507731,
          "running_time_in_nanos": 26042617305,
          "cancellable": true
        }
      }
    }
  }
}
```

### Result

I advise to start the delete query in a GNU Screen session. The end of the task will give you this exemplary output:

```json
{
  "took": 33658,
  "timed_out": false,
  "total": 424578,
  "deleted": 424578,
  "batches": 425,
  "version_conflicts": 0,
  "noops": 0,
  "retries": {
    "bulk": 0,
    "search": 0
  },
  "throttled_millis": 0,
  "requests_per_second": -1.0,
  "throttled_until_millis": 0,
  "failures": []
}
```
