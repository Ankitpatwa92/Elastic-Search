## Elastic Search Query Concept

### Term Query

Text fields are analyzed. This means that their values are first passed through an analyzer to produce a list of terms, which are 
then added to the inverted index.
There are many ways to analyze text: the default standard analyzer drops most punctuation, breaks up text into individual words, 
and lower cases them. For instance, the standard analyzer would turn the string “Quick Brown Fox!” into the terms [quick, brown, fox].

#### Result will found

```
POST _search
{
  "query": {
    "term": {
      "value": "quick"
    }
  }
}
```
#### Cases where result will not found

```
{
  "query": {
    "term": {
      "value": "Quick"
    }
  }
}
```
####  In Above query Quick not in lower case

```
{
  "query": {
    "term": {
      "value": "quick brown"
    }
  }
}
```
#### In Above query sentance is used in term query to seach insted of single token

```
{
  "query": {
    "term": {
      "value": "!"
    }
  }
}
```
#### In Above query ! mark is used for search but standard analyzer break sentance with punuation marks 


### Match Phrase
 query will analyze the input if analyzers are defined for the queried field and find documents matching the following criterias
 
All the search terms must appear in the field
All the search terms must have the same order as the input value
Match Phrase query is not case sensitive

For example, if you index the following documents (using standard analyzer for the field foo):

```
{ "foo":"I just said hello world" }

{ "foo":"Hello world" }

{ "foo":"World Hello" }
```

This match_phrase query will only return the first and second documents :
```
POST _search
{
  "query": {
    "match_phrase": {
      "foo": "Hello World"
    }
  }
}
```

This match_phrase query will also return result because standard analyzer will remove all punctuation mark !@#$%^&*()
```
POST _search
{
  "query": {
    "match_phrase": {
      "foo": "hello !@#$%^&*() world"
    }
  }
}
```

### Query String query

This will divide entire sentance into token and the search each token regardless of order and case

```
{ "foo":"I just said"}

{ "foo":"Hello world" }

{ "foo":"World Hello" }
```
POST _search
{
   "query": {
        "query_string" : {
            "query" : "I worl hello" 
        }
    }
}

It will return all document 


### Match Query
This will divide entire sentance into token and the search each token regardless of order and case (Need to find out difference between
query_string and Match Query)
```
POST _search
{
    "query": {
        "match": {
            "title": "HELLO"
        }
    }
}
```


### Range Query

```
GET _search
{
    "query": {
        "range" : {
            "age" : {
                "gte" : 10,
                "lte" : 20,
                "boost" : 2.0
            }
        }
    }
}
```

### Difference between term query and match query and match pharase query
```
Data :"This is your Company"

term query search only particular term not sentence   this,is,your,company
Match Quuery: This is your Company,  This IS YOUR Company, Company This is yOUR sss,is your,company   <case insensitive> <Order does not matter>
Match Phrase: This is your Company, This is ,is your,your   <case insensitive>   <Order Matter> <Match Exact Phrase>
```
