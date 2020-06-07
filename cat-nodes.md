Back to [Main](README.md)

# Nodes

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
