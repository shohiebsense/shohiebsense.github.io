Combining where clause and order clause is one thing.  

But what about when the search result requires you to have a degree of relevance, and at the same time you have to maintain the performance...(?)  

Postgre offers Text-Search Types  

Just take a look at [its documentation](https://www.postgresql.org/docs/current/datatype-textsearch.html):  

```
PostgreSQL provides two data types that are designed to support full-text search, which is the activity of searching through a collection of natural-language documents to locate those that best match a query. The tsvector type represents a document in a form optimized for text search; the tsquery type similarly represents a text query.
```

Just go and find out.  

At least I have two references to start with:

[this guy](https://medium.com/geekculture/comprehend-tsvector-and-tsquery-in-postgres-for-full-text-search-1fd4323409fc). 

[this guy](https://www.opsdash.com/blog/postgres-full-text-search-golang.html).  

[this official documentation](https://www.postgresql.org/docs/current/textsearch-controls.html)  

From those references, they give you each the option to make the where clause for searching;  

This approach:  

```sql
SELECT
  workid, act, scene, description, body, ts_rank(tsv, q) as rank
FROM
  scenes, plainto_tsquery('heaven earth') q
WHERE
  tsv @@ q
ORDER BY
  rank DESC
LIMIT
  10;
```   

Or this approach:  

```
select file_id, content from document_text where to_tsvector(content) @@ to_tsquery('(!bear & predict)| instruments');
```  

Or you want to use ranking approach. 

```
WHERE (ts_rank_cd(your_ts_vector_column, to_tsquery('``:*&term1:*&term2:*|term3:*')) > 0 )
```


So as you can see they support regex/wildcards, and the | or & are self-explanatory.  

go and find out yourself which one is better for you...  

just make sure that your query should ignore case and common cases to handle non-word letters (what is it called? There is a term for it in Language Science and in Natural Language Processing). 


