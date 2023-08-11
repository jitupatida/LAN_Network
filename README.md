In the given lab scenario , the objective is to establish connectivity between three routers, each connected to a switch, and two PCs connected to each switch. The routers are assigned specific IP addresses on their interfaces, and the PCs are configured with IP addresses and default gateways accordingly.

To achieve connectivity between the networks, we need to typically configure OSPF as the dynamic routing protocol on each router. OSPF would then exchange routing information with neighboring routers and build the routing table based on the network topology and learned routes. Here's a step-by-step overview:

Configuring OSPF: On each router, I enable OSPF and assign the respective router IDs. I also specify the networks to be advertised by OSPF using network commands, indicating which interfaces participate in OSPF routing.

Establishing OSPF Neighbor Relationships: OSPF routers discover neighboring routers by exchanging Hello packets. Once the routers detect each other's Hello packets and match the OSPF settings (area ID, authentication, etc.), they establish neighbor relationships.

Exchanging Link-State Advertisements (LSAs): OSPF routers exchange LSAs, which contain information about the router's directly connected networks and their associated metrics. LSAs are flooded throughout the OSPF area, ensuring that all routers have a consistent view of the network topology.

Building the Link-State Database (LSDB): Each router builds its LSDB by collecting and storing the LSAs received from neighboring routers. The LSDB contains information about the entire OSPF network's topology.

Running the Dijkstra Algorithm: OSPF routers run the Dijkstra algorithm using the LSDB to calculate the shortest path tree to all known networks. This calculation determines the best paths for packet forwarding based on the accumulated link costs.

Building the Routing Table: Based on the Dijkstra algorithm's results, each router builds its routing table. The routing table includes entries for destination networks, next-hop routers, and associated metrics (costs). The router selects the best path for each destination based on the lowest cumulative cost.

With OSPF in place, the routers can now efficiently route packets between the different networks. The routing table allows each router to determine the optimal path for forwarding packets based on the network topology and the dynamically learned routes.


Now , connecting all the above information with the provided data , we have three routers with switches connected to each router, and two PCs connected to each switch. Here's how OSPF operates and builds the routing table based on the provided information:

Router 1:
Left side interface: IP address 10.1.1.100
Command:
en
config t
int g0/0
ip add 10.1.1.100 255.0.0.0
no sh

Right side interface: IP address 20.1.1.1
command:
en
config t
int g0/1
ip add 20.1.1.1 255.0.0.0
no sh



Router 2:
Left side interface: IP address 20.1.1.2
command:
en
config t
int g0/0
ip add 20.1.1.2 255.0.0.0
no sh


Right side interface: IP address 40.1.1.1
command:
en
config t
int g0/1
ip add 30.1.1.100 255.0.0.0
no sh


Down side interface: IP address 30.1.1.100
command:
en
config t
int g0/2
ip add 40.1.1.1 255.0.0.0
no sh


Router 3:
Left side interface: IP address 40.1.1.2
command:
en
config t
int g0/0
ip add 40.1.1.2 255.0.0.0
no sh


Right side interface: IP address 50.1.1.100
command:
en
config t
int g0/1
ip add 50.1.1.100 255.0.0.0
no sh



To establish connectivity between these networks, I configure OSPF on each router. Also, all interfaces participating in OSPF are in the same OSPF area.

OSPF Configuration on Router 1:
command:-
router ospf 1
network 10.1.1.0 0.255.255.255 area 0
network 20.1.1.0 0.255.255.255 area 0


OSPF Configuration on Router 2:
command:-
router ospf 1
network 20.1.1.0 0.255.255.255 area 0
network 40.1.1.0 0.255.255.255 area 0
network 30.1.1.0 0.255.255.255 area 0


OSPF Configuration on Router 3:
command:-
router ospf 1
network 40.1.1.0 0.255.255.255 area 0
network 50.1.1.0 0.255.255.255 area 0



Once OSPF is configured, the routers will exchange OSPF Hello packets to discover neighboring routers and establish neighbor relationships.

Router 1 will establish a neighbor relationship with Router 2 over the right side interface (20.1.1.1).
Router 2 will establish a neighbor relationship with Router 1 over the left side interface (20.1.1.2).
Router 2 will also establish a neighbor relationship with Router 3 over the down side interface (30.1.1.100).
Router 3 will establish a neighbor relationship with Router 2 over the right side interface (40.1.1.1).
As OSPF neighbor relationships are established, the routers will exchange Link-State Advertisements (LSAs) containing information about their directly connected networks.

Router 1 will advertise the network 10.1.1.0/24 (connected to the left side interface) and receive LSAs from Router 2 for the networks 20.1.1.0/24 (connected to the right side interface of Router 2) and 30.1.1.0/24 (connected to the down side interface of Router 2).
Router 2 will advertise the networks 20.1.1.0/24 (connected to the left side interface), 30.1.1.0/24 (connected to the down side interface), and 40.1.1.0/24 (connected to the right side interface) and receive LSAs from Router 1 and Router 3 for their respective networks.
Router 3 will advertise the networks 40.1.1.0/24 (connected to the left side interface) and 50.1.1.0/24 (connected to the right side interface).
As the LSAs are flooded throughout the OSPF area, each router builds its Link-State Database (LSDB), which contains information about the network topology.

Based on the LSDB, each router runs the Dijkstra algorithm to calculate the shortest path tree and determine the best paths to reach different networks.

Router 1 will learn the shortest paths to the networks 20.1.1.0/24, 30.1.1.0/24, 40.1.1.0/24, and 50.1.1.0/24.
Router 2 will learn the shortest paths to the networks 10.1.1.0/24, 30.1.1.0/24, 40.1.1.0/24, and 50.1.1.0/24.
Router 3 will learn the shortest paths to the networks 10.1.1.0/24, 20.1.1.0/24, 30.1.1.0/24, and 50.1.1.0/24.
Finally, each router builds its routing table based on the shortest path calculations.

Router 1 will have entries in its routing table for the networks 20.1.1.0/24, 30.1.1.0/24, 40.1.1.0/24, and 50.1.1.0/24 with their respective next-hop addresses.
Router 2 will have entries for the networks 10.1.1.0/24, 30.1.1.0/24, 40.1.1.0/24, and 50.1.1.0/24.
Router 3 will have entries for the networks 10.1.1.0/24, 20.1.1.0/24, 30.1.1.0/24, and 50.1.1.0/24 with their respective next-hop addresses.
These routing table entries allow the routers to forward packets between different networks based on the optimal paths determined by OSPF.

To see the ospf database , we use the command 
sh ip ospf database

To see the protocol used in the router , we use the command
sh ip protocol

To see the ospf neighbor , we use the command
sh ip ospf neighbor


Thank you ! That's all from my side.

 