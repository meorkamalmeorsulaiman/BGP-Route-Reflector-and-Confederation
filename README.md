# BGP Route-Reflector and Confederation
This lab explore the fundamentals of Route Reflector and Confederation in BGP to help reduce the mesh overhead in iBGP.

## Route Reflector
Implementing Route Reflector is not a straight-forward method. You need to consider several rules when implementing Route Reflector such as:
* Update received by Route Reflector (RR) from non-RR client with be advertise to RR-client.
* Update received by RR from RR-client will be advertise to non-RR client and RR-client.
* Update received by RR from eBGP peer will be advertise to RR-client and non-RR client.
* Example config on R3 as a RR and R2 is a client:
  * neighbor 1.23.1.2 route-reflector-client (under router BGP command)
  * Route reflector reflect the configuration itself.

## BGP Confederation
BGP Confederation is as nested ASs or AS within an AS. An AS will contain sub-ASs with a private AS number. All peer in sub-ASs need to be fully mesh or route-reflector can be implemented. Same rules of iBGP applied to sub-ASs.
* Example configuration on R8 (under router bgp command)
  * router bgp 65100
  * bgp confederation identifier 300
  * bgp confederation peers 65200 

![alt text](https://github.com/meorkamalmeorsulaiman/BGP-Route-Reflector-and-Confederation/blob/main/Topology.PNG)

## Lab Details:
* BGP
  * Transit ASs are AS200 and 300.
  * Route-reflector implemented in AS200.
  * BGP Confederation implemented in AS300.
  * AS65200 is a full mesh iBGP.
 
* Overlay Routing
  * EIGRP - AS200
  * OSPF - AS300
