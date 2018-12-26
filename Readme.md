# Elastic Search Important Queries

### Delete data of types in index without deleting index and type

```
POST twitter,blog/_docs,post/_delete_by_query
{
  "query": {
    "match_all": {}
  }
}
```

### Get all Index List
```
http://elasticServerIP:9200/_cat/indices?v
```

### Search By Index name Type name

```
http://elasticServerIP:9200/index/type/_search

```

### Search any value in Elastic Seach
```
http://elasticServerIP:9200/_search?q=searchvalue
```

### Elasric Create Index Query

```
PUT twitter
{
    "settings" : {
        "index" : {
            "number_of_shards" : 3, 
            "number_of_replicas" : 2 
        }
    }
}
```

### Delete index query

```
Delete                  //Http Method
http://elasticServerIP:9200/indexName   //Delete Particular index  

http://elasticServerIP:9200/indexName/type   //Delete Particular type in index

```

### Elastic Search Bool query

```
POST _search
{
  "query": {
    "bool" : {
      "must" : {
        "term" : { "user" : "kimchy" }
      },
      "must_not" : {
        "range" : {
          "age" : { "gte" : 10, "lte" : 20 }
        }
      },
      "should" : [
        { "term" : { "tag" : "wow" } },
        { "term" : { "tag" : "elasticsearch" } }
      ],
      "minimum_should_match" : 1,
      "boost" : 1.0
    }
  }
}

```

### Elastic Search Partial Update Record
```
POST test/_doc/1/_update
{
    "doc" : {
        "name" : "new_name"
    }
}
```
