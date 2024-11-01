From polar-it on Discord

There is a lot to add to this to fill details, however this is enough for people familar to get going ;)

If you are not familar with HAProxy then check it out if you're a sysadmin/devops person it is pretty great. If you are a Containers / Kubernetes kind of person then this kind of thing is handle by the load balancers, sometimes they are HAProxy under the covers.

```
#---------------------------------------------------------------------
# main frontend which proxys to the backends
#---------------------------------------------------------------------
frontend  main *:11898

    default_backend            dego-daemon

#---------------------------------------------------------------------
# round robin balancing between the various backends
#---------------------------------------------------------------------
backend dego-daemon
    balance     roundrobin
    option httpchk GET /info
    http-check expect rstring true

# Local node on port 11999
    server  app1 127.0.0.1:6969 check
    server  app2 < node host1 >:6969 check
    server  app3 < node host2 >.6969 check
    server  app4 < node host3 >:6969 check
```

_**Ole Cuvee** This can work with nginx-based loadbalancing too, and it powers nodes that run DeroGold Explorer at https://explorer.derogold.online_
