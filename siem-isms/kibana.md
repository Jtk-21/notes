# Kibana

## Dev Tools

##### Re-Index Data Into New Index
```
POST _reindex
  {
    "Source": {
      "index": "my-index"
    }
    "Dest": {
      "index": "new-index"
    }
  }
```
