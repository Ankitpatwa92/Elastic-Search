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
