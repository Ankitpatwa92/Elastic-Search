###How to restirct unknown fields
```
set "dynamic": "strict" in mapping
```

### Differnece between filter and query

```
Filters -> Does this document match? a binary yes or no answer  filter data are cached

Queries -> Does this document match? How well does it match? uses scoring

```


### How to make es backup?

//Create Repo
```
#curl -XPUT -H "Content-Type: application/json;charset=UTF-8" 'http://localhost:9200/_snapshot/esbackup' -d '{
  "type": "fs",
  "settings": {
     "location": "/elasticseacrhData/es-backup",
     "compress": true
  }
}
```

//Create snapshot
PUT
http://localhost:9200/_snapshot/esbackup/my_snapshot?wait_for_completion=true"

//Create entry in es
path.repo: '/opt/elasticsearch-5.5.0/esbackup'

 //Restore
 
 Create Repo on restoring system and then restore also provide path of repo
 
 curl  -XPOST "http://localhost:9200/_snapshot/esrestore/linuxpoint_snapshot/_restore?wait_for_completion=true"
