`docker container -p` we know it exposes the port on our machine.  

quick port check with `docker container port <container_name>`  

by default, each container connected to a private network `bridge`  

to make it interconnected through public network (internet) it routes out through NAT firewall, and its configurable through docker daemon  

we can attach containers to more than one virtual network,  

or we can skip virtual networks and use the host IP using `--net=host`  

also by default, from machine to container, there is a ... let's called a firewall that blocks the incoming traffic.  

to see list of network `docker network ls`  

to inspect a network `docker network inspect`  

to create a network `docker network create --driver`  

to attach a network to container(s) `docker network connect`. 

to detach `docker network disconnect`. 
