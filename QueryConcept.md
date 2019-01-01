## Elastic Search Query Concept

### Term Query

Text fields are analyzed. This means that their values are first passed through an analyzer to produce a list of terms, which are 
then added to the inverted index.
There are many ways to analyze text: the default standard analyzer drops most punctuation, breaks up text into individual words, 
and lower cases them. For instance, the standard analyzer would turn the string “Quick Brown Fox!” into the terms [quick, brown, fox].

#### Result will found

```
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



