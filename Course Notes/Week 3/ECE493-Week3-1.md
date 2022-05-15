# ECE493 Week 3 Part 1: Transport Layer

- [ECE493 Week 3 Part 1: Transport Layer](#ece493-week-3-part-1-transport-layer)
  - [Transport Layer Objectives](#transport-layer-objectives)
    - [Congestion Control](#congestion-control)
    - [Reliable Transport](#reliable-transport)
    - [(De)multiplexing](#demultiplexing)
    - [Loss Recovery](#loss-recovery)
  - [Transport Layer Techniques](#transport-layer-techniques)
    - [Pump Slowly, Fetch Quickly (PFSQ)](#pump-slowly-fetch-quickly-pfsq)
    - [Event-to-Sink Reliable Transport (ESRT)](#event-to-sink-reliable-transport-esrt)
  - [Why not TCP?](#why-not-tcp)
  - [Why not UDP?](#why-not-udp)

## Transport Layer Objectives
- The success and efficiency of WSNs directly depend on reliable communication between sensor nodes and the sink.
- In a multi-hop, mulit-sensor environment, a reliable transport mechanism is imperative.
- The main objects of a transport layer protocol for WSNs are as follows:

### Congestion Control
- Packet losses due to congestion can impair reliability at the sink, even when enough info is sent out by the sources.
- Congestion control is an important component of the transport layer to achieve the required reliability.
- Congestion control not only increases the network efficiency, but also helps conserve scarce sensor resources.
- There are 2 main causes for congestion:
  - Packet arrival rate exceeding packet service rate (more likely at nodes closer to the sink)
  - Link level performance such as contention, interference and bit error.
- Three methods can be used to control congestion:
  - Congestion detection
    - Monitor queue length, packet service time and the ratio between packet service time and packet inter-arrival time at an intermediate node
  - Congestion notification
    - Inform the nodes
    - Explicit or implicit notification
  - Rate Adjustment
    - Nodes adjust their traffic sending rate
    - AIMD (Additive Increase Multiplicatvie Decrease) schemes.

### Reliable Transport
- Based on application requirements, the extracted event features should be reliably transferred to the sink.
- The programming/retasking data for sensor operation, command and queries should be reliably delivered to the target sensor nodes to assure proper WSN function.

### (De)multiplexing
- Different applications can be served on sensor nodes through the same network.
- The transport layer should bridge the application and network layers by using multiplexing and demultiplexing.

### Loss Recovery
- Loss detection and notification
  - Usual approach -> sequence numbers
  - End-to-end -> Like in TCP
  - Hop-by-hop -> Receiver based or sender based
- Retransmission-based loss recovery
  - End-to-end -> Like in TCP, expensive
  - Hop-by-hop -> Nodes need to cache
    - Much more energy efficient

## Transport Layer Techniques

### Pump Slowly, Fetch Quickly (PFSQ)
- Introduced to distribute data from a source node by injecting packets into the network at relatively low speed (pump slowly)
- Allows nodes that experience data loss to aggressively recover missing data from their neighbours (fetch quickly)
- The goals of PSFQ are:
  - Ensure that all data segments are delivered to the intended destinations with minimum special requirements on the nature of the lower layers
  - Minimize number of transmissions to recover lost information
  - Operate correctly even in situations where the quality of the wireless links is very poor
  - Provide loose delay bounds for data delivery to all intended receivers
- PFSQ ais to guarantee sensor-to-sensor delivery and to provide end-to-end reliability for control management distribution from the control node (sink) to the sensors.
- Note that PSFQ does not address congestion control.

### Event-to-Sink Reliable Transport (ESRT)
- Aims to achieve reliable event detection at the sink node based on a protocol that is energy aware and which can control congestion.
- Important features of ESRT are:
  - **Self-configuration**, even in the case of a dynamic topology
  - **Energy awareness**, sensor nodes are notified to decrease their reporting frequency if the reliability level at the sink node is above the minimum.
  - **Congestion Control**, takes advantage of the high level of correlation between the data flows corresponding to the same event
  - **Collective Identification**, sink is only interested in the collective information from a group of sensors not in their individual reports
  - **Biased implementation**, most of the complexity of the protocol falls on the sink node minimizing the requirements on the sensor nodes.

## Why not TCP?
- TCP is unable to distinguish between congestion losses and transmission losses, causing poor performance
- TCP is not suitable for wireless multi-hop
- TCP provides 100% reliability, which is overkill for many applications
- TCP is connection-oriented, and can thus be expensive and unnecessary
- TCP depends on network-wide unique addresses of nodes
- Preprocessing or aggregation of data in intermediate nodes is desirable and often necessary
  - Packets can often be combined or changed before they reach their final destination.
- TCP is not light-weight, and has too much overhead.

## Why not UDP?
- No reliability at all (EASY!)