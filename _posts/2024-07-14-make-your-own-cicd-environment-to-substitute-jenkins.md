So I think to use jenkins and similar are somehow cumbersome, feels like too fancy for me.  

I come up with making own CICD Process. Stuff I use:  
  
- Nginx for reverse proxy, any api gateway would do
- Discord, a channel with a webhook
- Python, to execute shell commands
- Repository, a guinea pig that you want to implement these pipeline works
- Github actions, to trigger an event when a specific branch is updated
- Git, with handling the credentials cached.
- Docker (to be honest writing it to the list is a bit irrelevant, but when it comes to update the image and to redeploy again, to containerize again, you got the idea).  
  
So far so good, better at controlling, it complies, just what I need. I feel good building this...
