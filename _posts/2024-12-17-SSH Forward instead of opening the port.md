Your database part, let's say is 5432 or 6371.  

One of the easy ways is that you can make your server make its ports public.  

But this approach will get you in trouble. Security breach and stuff.  

Use `Port Agent Forwarding` instead.

ChatGPT:

```
The -A flag in SSH is used to enable agent forwarding. When you use this option, the SSH agent (which holds your private keys for authentication) is forwarded to the remote machine. This allows you to use your local SSH keys on the remote machine to authenticate to other servers or systems.
```

say your ssh port is 6767, usually 22 isnt it

```
ssh -A -p 6767 root@IP.Server.Address.orhostname -N -L 6001:0.0.0.0:6001
```

Flags
```
The -N option tells SSH not to execute any commands on the remote server. It is primarily used when you only need to establish a tunnel or port forwarding.

Use Case:
You just want to forward ports without starting an interactive shell or running any commands.

The -L option is used for local port forwarding. It forwards a local port to a specific host and port on the remote server.

Syntax
-L [local_port]:[remote_host]:[remote_port]
```
