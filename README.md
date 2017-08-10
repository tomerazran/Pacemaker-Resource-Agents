# Pacemaker-Resource-Agents
Pacemaker Cluster Resource Agents
-----------------------------------

This repo contains pacemaker cluster resource agents (RA):

  1) ipspeed - a resource agent that mesure the speed for interfaces that can hold an ip address. I needed this resource since I use a virtual IP address (IPaddr2 RA) with bonded interfaces. The problem is that when the bond is non-functional, the cluster does not failover the resource to the other node. I posted a question on the packmaker mailing list (http://lists.clusterlabs.org/pipermail/users/2017-August/006224.html). Thanks to Vladislav Bogdanov <bubble@hoster-ok.com> which gave me a tip to use the ifspeed RA. The ipspeed RA is based on the ifspeed RA, but with one change - it will try to determine the interfae to messure based on a IP address parameter.
  
  In order to use this RA effectively, you will have to create a location constraint:
    
     # pcs resource create vip ocf:heartbeat:IPaddr2 ip=192.168.1.3 op monitor interval=30
     # pcs resource create vip_speed ocf:heartbeat:ipspeed ip=192.168.1.3 name=vip_speed op monitor interval=5s --clone
     # pcs constraint location vip rule score=-INFINITY vip_speed lt 1 or not_defined vip_speed

