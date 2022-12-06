
Instead of revert, if you would like to delete a pushed commit, 
Go to settings / preferences -> search `optimize imports` then you will see `optimize imports on fly`, you can configure the rest.

1. do:

   ```git
       git reset --soft HEAD~2 //number of commit you want to delete
   ``` 

2. The state is back to where you haven't pushed yet, don't pull it.

3. do:
   ```git
       git push origin +master --force 
   ```
   or your `+desired branch`
