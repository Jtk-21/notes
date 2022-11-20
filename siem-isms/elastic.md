# Elastic

## Curl Elastic
`curl -XGET http://elasticsearchIP:9200/`

`_cat/indices?pretty` get indices listing `_cat/indices/<index_name>` specific index info

`_cluster/health?pretty` get cluster health info

`_cat/shards` get shards `_cat/shards/<shard name>` specific shard info

`_cat/allocation/*?v` node allocation info

`_nodes/stats` node stat info

`_cluster/settings` get cluster settings

`_cat/nodes` get nodes

`_cluster/allocation/explain?pretty` detailed cluster allocation info

`_recovery`

`_cat/master`

`_cluster/health?level=indices`

`_cluster/health?level=shards`
