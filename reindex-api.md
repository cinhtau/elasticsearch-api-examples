# Reindex Data

* TOC
{:toc}

## Reduce Shards

Reindex to reduce shards, create target index with specific settings:

```bash
curl -XPUT "http://localhost:9200/fo-log-re-2017.06.18" -H 'Content-Type: application/json' -d'
{
  "settings": {
    "number_of_shards": 1,
    "number_of_replicas": 0,
    "routing": {
      "allocation": {
        "require": {
          "box_type": "warm"
        }
      }
    }
  },
  "mappings": {
    "logs": {
      "properties": {
        "cardOppPlbAuthTime": {
          "type": "keyword"
        }
      }
    }
  }
}'
```

Basic reindex example
```bash
curl -XPOST 'localhost:9200/_reindex?pretty' -H 'Content-Type: application/json' -d'
{
  "source": {
    "index": "fo-log-2017.06.18"
  },
  "dest": {
    "index": "fo-log-re-2017.06.18"
  }
}
'
```

## Reindex Asynchronously

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

## Check Tasks

Check or list running reindex tasks

```
GET /_tasks/?pretty&detailed=true&actions=*reindex
```

See also this [blog article](https://cinhtau.net/2016/09/19/reindex-data-in-elasticsearch/).
