## Elastic Search Query Concept

### Term Query

Text fields are analyzed. This means that their values are first passed through an analyzer to produce a list of terms, which are 
then added to the inverted index.
There are many ways to analyze text: the default standard analyzer drops most punctuation, breaks up text into individual words, 
and lower cases them. For instance, the standard analyzer would turn the string “Quick Brown Fox!” into the terms [quick, brown, fox].

If we search with Quick then result will not found because default analyzer convert all values in lower ase
```
{
  "query": {
    "term": {
      "value": "Quick"
    }
  }
}
```

Correct search query

```
{
  "query": {
    "term": {
      "value": "quick"
    }
  }
}
```

