# OSPF Multiarea Labs

OSPF is a link-state routing protocol that uses the Shortest Path First (SPF) / Dijkstra's algorithm to prevent routing loops and calculate the most efficient paths.

Each router advertises its local link states via Link-State Advertisements (LSAs), which are flooded throughout the area so every node can construct an identical Link-State Database (LSDB) representing the entire network topology.

Using this LSDB as a map, each router runs Dijkstra's algorithm placing itself as the root vertex (V0​) to calculate a loop-free, shortest-path tree based on the cumulative link cost (where Cost=Interface BandwidthReference Bandwidth​), injecting the optimal routes into the routing table.


## Network Topology

![Image](https://github.com/hellopijo/packet-tracer-labs/blob/main/ospf-multiarea/ospf_topology)


## IP Tables
| Device | Interfaces | IP Address | Subnet Mask | Area |
| --- | --- | --- | --- | --- | 
| R1 | G0/0 | 10.10.1.1/30 | 255.255.255.252 | 0 | 
|  | G0/1 | 10.0.1.2/30 | 255.255.255.252 |
|  | G0/2 | 10.0.3.2/30 | 255.255.255.252 |
| R2 | G0/0 | 10.10.1.2/30 | 255.255.255.252 | 10 |
|  | G0/1 | 10.10.2.1/24 | 255.255.255.0 |
| R3 | G0/0 | 10.0.1.1/30 | 255.255.255.252 | 0 |
|  | G0/1 | 10.0.2.1/30 | 255.255.255.252 |
| R4 | G0/0 | 10.0.3.1/30 | 255.255.255.252 | 0 |
|  | G0/1 | 10.0.2.2/30 | 255.255.255.252 |
|  | G0/2 | 10.20.1.1/30 | 255.255.255.252 |
| R5 | G0/0 | 10.20.1.2/30 | 255.255.255.252 | 20 |
|  | G0/1 | 10.20.2.1/30 | 255.255.255.252 |
| R6 | G0/0 | 10.20.3.1/24 | 255.255.255.0 | 20 | 
|  | G0/1 | 10.20.2.2/30 | 255.255.255.252 |
| PC-A | FA0 | 10.10.2.2/24 | 255.255.255.0 | 10 |
| PC-B | FA0 | 10.20.3.2/24 | 255.255.255.0 | 20 | 
| PC-C | FA0 | 10.20.3.3/24 | 255.255.255.0 | 20 |

## What i done?
Basically what i done is configuring OSPF for all these routers. I used multiarea to reduce the loads that need to be handle by each routers by separate it to 3 area (area 0, area 10, area 20). R1 and R4 works as ABR (Area Border Router) which connect one or more areas to the OSPF backbone. Every router be assigned router id based on its names as example, `R1 - 1.1.1.1` . 

## Results

<img width="729" height="128" alt="image" src="https://github.com/user-attachments/assets/ecd0bb53-3095-469a-825b-d2b4320656f3" />

<img width="728" height="114" alt="image" src="https://github.com/user-attachments/assets/a54fce7d-b603-46cf-bb4c-020fab67674a" />

<img width="728" height="114" alt="image" src="https://github.com/user-attachments/assets/273983fb-1ce0-4b5a-b3fb-1b399ba9a705" />

<img width="774" height="617" alt="image" src="https://github.com/user-attachments/assets/c5295b7b-1ea7-4549-b6d4-6043adefeec6" />
