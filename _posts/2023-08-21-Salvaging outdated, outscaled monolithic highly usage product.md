It was from April, I got an opportunity to lead mentally exhausted team, in technical aspects, architectures along with flows of the product.  

It is an old, gold jquery php codeigniter3 mysql stacks with monolithic-based server. It is not them to build, we are just continuing, leaving these the big homeworks to us. 

It relies so much on Queries, a big deal amount of joins, let alone the subqueries, views with already packed up with > 5 joins.  

Also with procedures that has 4 UNIONS man, Imagine.  

Simply it is awful enough, that makes some data can finally displayed for almost one minute.  

Numerous Approach have been taken :

1. Forwarding some heavy queries to Golang as a backend to enable asynchronous by using the existing PHP as the proxy.  
2. Combining multiple tables (not join) from the memory layer rather than in the disk-storage, database-read UNION layer.  
3. Implementing Web Server's load-balance to 3 different ports round robin.  
4. Restructuring Git workflow and pipeline to improve the team's performance.  
5. Using the window function rather than the traditional double query to count all the data and the data itself. So that it can be executed in a single query.  
6. Optimizing query by only selecting the data that need to be displayed rather than all the columns.  
7. Implementing web server's cache for style and javascript asset files.  
8. Remove the queries that have the self-joined approach, and rewrite them to the optimized ones.  
9. Refactor numerous app controller functions to become a single responsibility pattern.
10. Retrospective sessions where team members said something that has been bottled for the long time.

The result is not bad though, is quite impressive. 
Not only can the data be displayed in under 3 seconds, but we've also received noteworthy positive feedback from customers. Let's not overlook the team's high level of engagement. We return even more eager to acquire knowledge and visibly enhanced skills.
