---
title: Task Management
description: Manage tasks within Elasticsearch
---

## List all tasks

```
GET _tasks?detailed=true
```

## Cancel one task

```
POST _tasks/node_id:task_id/_cancel
```
