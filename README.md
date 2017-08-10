# Pacemaker-Resource-Agents
Pacemaker Cluster Resource Agents
-----------------------------------

This repo contains pacemaker cluster resource agents (RA):

  1) ipspeed - a resource agent that mesure the speed for interfaces that can hold an ip address. I needed this resource since I use a virtual IP address (IPaddr2 RA) with bonded interfaces. The problem is that when the bond is non-functional, the cluster does not failover the resource to the other node. I posted a question on the packmaker mailing list (http://lists.clusterlabs.org/pipermail/users/2017-August/006224.html). Thanks to Vladislav Bogdanov <bubble@hoster-ok.com> which gave me a tip to use the ifspeed RA. The ipspeed RA is based on the ifspeed RA, but with one change - it will try to determine the interfae to messure based on a IP address parameter.
