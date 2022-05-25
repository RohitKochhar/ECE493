# Assignment 1

Group Members: Rohit Singh (20718756) 

- [Assignment 1](#assignment-1)
  - [Problem 1](#problem-1)
    - [IEEE 802.15.4](#ieee-802154)
      - [Stack Layer](#stack-layer)
      - [Standard](#standard)
      - [Data Rate](#data-rate)
      - [Range](#range)
      - [Frequency Band](#frequency-band)
      - [Topology](#topology)
      - [Power Requirements](#power-requirements)

## Problem 1
For each one of the following IoT protocols, determine what later of the IoT stack it belongs to, and describe its characteristics with respect to: standard, data rate, range, frequency band, topology, and power requirements

### IEEE 802.15.4

References:
- A. Koubaa, M. Alves and E. Tovar, *IEEE 802.15.4 for Wireless Sensor Networks: A Technical Overview*, 2005

#### Stack Layer

- The IEEE 802.15.4 protocol specified the Medium Access Control (MAC) sub-layer and physical layer for Low-Rate Wireless Private Area Networks.

#### Standard

#### Data Rate

#### Range

#### Frequency Band

#### Topology

- There are three basic types of network topologies defined in the IEEE 802.15.4 standard:

  1. The *star* topology
     - Here, a unique node operates as a *personal area network* (PAN) *coordinator*, providing synchronization services through the transmission of beacons. 
       - This PAN coordinator is typically a *full function device* (FFD) which when activated can establish its own network and assume this role of coordinator.
       - Being the PAN coordinator is a higher-powered task, so often it is desirable to ensure the PAN coordinator is main powered rather than battery powered.
     - As other devices join the network, they must be willing to communicate with other devices by sending the data to the PAN coordiantor, who then dispatches the data to the adequate destination devices.
       - These new devices can either be *full* or *reduced* function (FFD and RFD, respectively.) 
       - Devices that assume this role do not necessarily need to be mains powered, and can instead be battery powered, allowing them to be more easily deployable to the field.
     - There are several consequences of the star topology however:
       - All sensor nodes are supposed to be battery-powered, and thus can be heavily resource constrained.
       - The PAN coordinator undergoes heavy resource usage, causing its battery resources to become rapidly ruined. 
     - As such, this specific topology is recommended for applications such as home automation, personal computer peripherals, toys and games. 


  2. The *peer-to-peer* topology 
       - Similarly to the star topology, the peer-to-peer topology also features a PAN coordinator, which is nominated by virtue of being the first device to communicate via the channel.
       - In contrast to the star topology which is centralized around the PAN coordinator however, the peer-to-peer network topology is decentralized and each device can directly communicate with any other device within its radio range.
         - This mesh-like topology allows for networking flexibility, however it incurs additional complexity for providing an end-toend connectivity between all devices belonging to the network.
       - Peer-to-peer topology operates in an ad-hoc fashion, allowing multi-hop routing between any two devices, but this functionality must be defined at the network layer, and as such, is not considered specifically in this specification.
       - This topology is recommended for wireless sensor networks, since resource usage is more evenly distributed across all nodes rather than replying on the PAN specifically.
  
  3. The *Cluster-Tree* topology
       - The cluster-tree topology is a specific case of the peer-to-peer topology, in which most devices are *full function devices*, allowing for multiple *virtual* PAN coordinators, which allows for the network to be distributed across multiple clusters, consisting of smaller peer-to-peer networks.
       - There is still only one single PAN coordinator for the overall network, but the other *virtual* PAN coordinators are instead referred to as *Cluster Heads* (CLH), with a key difference being that t       - Similarly to the star topology, the peer-to-peer topology also features a PAN coordinator, which is nominated by virtue of being the first device to communicate via the channel.
       - In contrast to the star topology which is centralized around the PAN coordinator however, the peer-to-peer network topology is decentralized and each device can directly communicate with any other device within its radio range.
         - This mesh-like topology allows for networking flexibility, however it incurs additional complexity for providing an end-toend connectivity between all devices belonging to the network.
       - Peer-to-peer topology operates in an ad-hoc fashion, allowing multi-hop routing between any two devices, but this functionality must be defined at the network layer, and as such, is not considered specifically in this specification.
       - This topology is recommended for wireless sensor networks, since resource usage is more evenly distributed across all nodes rather than replying on the PAN specifically.he PAN coordinators maintain the power to upgrade devices to become CLHs.




#### Power Requirements
