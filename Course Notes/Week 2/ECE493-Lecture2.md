# ECE493 Lecture 2: Simulation Tools

(May 9th, 2022)

- [ECE493 Lecture 2: Simulation Tools](#ece493-lecture-2-simulation-tools)
  - [Overview](#overview)
  - [OMNet++](#omnet)
    - [Modeling concepts](#modeling-concepts)
    - [Modules](#modules)
    - [Message, gets and links](#message-gets-and-links)
    - [OMNeT++ structure](#omnet-structure)
    - [Network Topology](#network-topology)

## Overview
- Wireless Sensor Network (WSN) Simulations can be categorized into two groups:
    - **Network Simulator**
      - Used to evalute the protocol performance
      - Examples are OMNET++, NS-3, and more
    - **Network Emulator**
      - Used to simulate the performance on the real hardware platform of WSN nodes.
      - Examples are TOSSIM, ATEMU and others.
- A possible quiz question could be to explain what a simulator is vs. an emulator and how the two work together to demonstrate the function of the whole WSN.

## OMNet++
- OMNet++ is a *simulator*
- It is **object oriented** and **modular**
- It can be used to simulate:
  - Modelling of *wired and wireless* communication networks
  - Protocol modelling
  - Modelling of queuing networks etc.

### Modeling concepts
- Modules communicate with message passing
- Active modules are called simple modules
- Messages are sent through output gates and received through input gates.
- I/O gates are linked through connection
- Simulation parameters such propagation delay, data rate and bit error rate, can be assigned to connections. So the reliability and latency of different communication mediums can be modelled accurately.

### Modules
- The top-level module is called the **system module**
- The contains **sub modules**
- Sub modules contain further sub modules.

### Message, gets and links
- Modules communicate by exhanging messages
- Messages can represent **frames or packets**
  - Frames consist of a sequence of packets
- Gates are the I/O interfaces of the module

### OMNeT++ structure
- `.ned` files define the topology
  - NED has several features which make it scale well to large projects, as it is hierarchical, component-based, as well as building on interfaces, inheritance, packages and metadata annotation.
- `.msg` files define the message structure
- `.cc/.h` files define the simple module sources
- When the program starts, all `.ned` files are read, along with a configuration file `omnetpp.ini`.
- Then the output is written into a result file, from which a graph is then generated.

### Network Topology
- Every network consists of:
  - Nodes
  - Gates
  - Connections




