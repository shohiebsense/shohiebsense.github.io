After you take which where clause that fits you the most,  

Then another thing to consider is where to put ts_vector exactly, is it in the table or in VIEW?  

Postgre also offers Materialized View, static view that offers faster search than vanilla VIEW.  

Keep in mind this requires REFRESH that locks all the tables during the process..  

Have a look at [the official documentation about materialized view](https://www.postgresql.org/docs/current/rules-materializedviews.html)  

After you have the conclusion about which one, next step is about the tsvector column itself.  

My Approach is like this:  


```
to_tsvector('english'::regconfig, concat_ws(' '::text, column1, column2 column3)) AS your_ts_vector_column
```
