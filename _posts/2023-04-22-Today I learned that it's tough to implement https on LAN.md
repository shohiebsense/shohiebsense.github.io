In go itself, gin to be precise, the default is using http.  

It would be not easy to deploy on LAN, where it gets accessed on another node.  

Modern browser itself atleast requires SSL and thats the minimum, to allow us to procceed (with risk, as it is self signed certificate).  

It is also different thing when it comes to deploy in http package and gin.  

In http, it's straight forward, you should have .crt and .key already and do

`server.ListenAndServeTLS("server.crt", "server.key")`  

In gin you have to explore further, until I write this post, still doesn't work.

Also for the connectivity test if the ping or telnet is not enough, you could try ncat, it's inside [nmap 7.92](https://stackoverflow.com/questions/63588254/how-to-set-up-an-https-server-with-a-self-signed-certificate-in-golang).  

7.93 the current latest until this posted, the ncat command had a bug. Just go to the previous one.  

the command: `ncat -vz ipaddr port`

the result  

```.sh
Ncat: Version 7.92 ( https://nmap.org/ncat )
Ncat: Connected to 192.168.1.3:61613.
Ncat: 0 bytes sent, 0 bytes received in 0.09 seconds.
```
