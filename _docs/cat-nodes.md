---
title: Nodes
description: View node details
---

## List Nodes

Get Elasticsearch version and Java Version of each node

```
GET /_cat/nodes?v&h=version,name,jdk
```

Output

```text
version name            jdk
5.3.1   ironman         1.8.0_121
5.2.2   hulk            1.8.0_121
5.3.1   captain_america 1.8.0_121
5.3.1   black_widow     1.8.0_121
5.3.1   thor            1.8.0_111
5.3.1   hawkeye         1.8.0_121
5.2.2   doctor_strange  1.8.0_121
5.3.1   scarlet_witch   1.8.0_121
5.3.1   vision          1.8.0_121
```

Get name, ip, port, version, jdk and master role
```
GET /_cat/nodes?v&h=name,ip,port,v,jdk,m
```

Helpful during rolling cluster upgrades
```text
name   ip          port v     jdk    m
uzuf73 172.25.0.73 9300 7.7.0 14     *
uzuf74 172.25.0.74 9300 7.7.0 14     -
uzuf72 172.25.0.72 9300 7.7.1 14.0.1 -
uzuf76 172.25.0.76 9300 7.7.1 14.0.1 -
uzuf75 172.25.0.75 9300 7.7.1 14.0.1 -
```
