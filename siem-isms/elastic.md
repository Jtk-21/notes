# Elastic

## Curl Elastic
`curl -XGET http://elasticsearchIP:9200/`

`_cat/indices?pretty` get indices listing `_cat/indices/<index_name>` specific index info

`_cluster/health?pretty` get cluster health info

`_cat/shards` get shards `_cat/shards/<shard_name>` specific shard info

`_cat/allocation/*?v` node allocation info

`_nodes/stats` node stat info

`_cluster/settings` get cluster settings

`_cat/nodes` get nodes

`_cluster/allocation/explain?pretty` detailed cluster allocation info

`_recovery`

`_cat/master`

`_cluster/health?level=indices`

`_cluster/health?level=shards`

## Open Index
`curl -XPOST http://elasticsearchIP:9200/<index_name>/_open` 

### Mass Retrieve & Open Indices
`curl -XGET http://elasticsearchIP:9200/_cat/indices/*?v | grep "red" | awk '{print $2}' > index.txt` get all index info - status 'red' - print index name to file

`while read -r line; do curl -XPOST http://elasticsearchIP:9200/$line/_open; done < index.txt` open every 'red' index from file

`curl -XPOST http://elasticsearchIP:9200/<index_name>/_open` open specified index
