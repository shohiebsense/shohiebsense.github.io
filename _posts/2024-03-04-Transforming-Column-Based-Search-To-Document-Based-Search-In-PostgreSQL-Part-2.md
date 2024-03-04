After you take which where clause that fits you the most, make your tsvector column to be indexed.  

`CREATE INDEX ts_vector_column ON "the_schema"."view_whatever" USING GIN(ts_vector_column);`

Then another thing to consider is where to put ts_vector exactly, is it in the table or in VIEW?  

Postgre also offers Materialized View, static view that offers faster search than vanilla VIEW.  

Keep in mind this requires REFRESH that locks all the tables during the process..  

Have a look at [the official documentation about materialized view](https://www.postgresql.org/docs/current/rules-materializedviews.html)  

To refresh concurrently, you have to make a Unique Index apart from GIN INDEX for the tsvector.  

`CREATE UNIQUE INDEX ON "the_schema"."view_whatever" (id);`

After you have the conclusion about which one, next step is about the tsvector column itself.  

My Approach is like this:  


```
to_tsvector('english'::regconfig, concat_ws(' '::text, column1, column2 column3)) AS your_ts_vector_column
```

