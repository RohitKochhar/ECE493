# ECE493 Week 3 Part 2: Application Layer and Messaging Protocols

- [ECE493 Week 3 Part 2: Application Layer and Messaging Protocols](#ece493-week-3-part-2-application-layer-and-messaging-protocols)
- [Application Layer](#application-layer)
  - [Application Layer Objectives](#application-layer-objectives)
  - [Sensor Management Protocol (SMP)](#sensor-management-protocol-smp)
  - [Simple Network Management Protocol (SNMP)](#simple-network-management-protocol-snmp)
  - [Management Protocol Requirements](#management-protocol-requirements)
  - [Functional Areas of Management Protocols](#functional-areas-of-management-protocols)
    - [Fault](#fault)
    - [Configuration](#configuration)
    - [Accounting](#accounting)
    - [Performance](#performance)
    - [Security](#security)
  - [Power Management](#power-management)
- [Messaging Protocols](#messaging-protocols)
  - [Process2Process Communication](#process2process-communication)
  - [Why not HTTP?](#why-not-http)
  - [MQTT](#mqtt)
    - [MQTT Architecture](#mqtt-architecture)
    - [MQTT Topics](#mqtt-topics)
    - [MQTT Messages](#mqtt-messages)
    - [MQTT QoS](#mqtt-qos)
    - [MQTT Advantages](#mqtt-advantages)
      - [Scalability](#scalability)
      - [Space decoupling](#space-decoupling)
      - [Time decoupling](#time-decoupling)
      - [Synchronization decoupling](#synchronization-decoupling)

# Application Layer

## Application Layer Objectives
- The application layer contains a variety of application layer protocols to generate various sensor network applications.
- The application layer performs various sensor network applications such as:
  - Query dissemination
  - Node localization
  - Time synchronization
  - Network security, authentication and key distribution
  - Sensor movement management

- As an example, the Sensor Management Protocol (SMP) is an application layer management protocol that provides software operations to perform tasks such as:
  - Location exchanging
  - Sensor node synchronization
  - Moving sensor nodes
  - Scheduling sensor nodes
  - Querying sensor node status
  - Controlling sensor node states

## Sensor Management Protocol (SMP)
- SMP is an application layer management protocol that makes the hardware and software of the lower layers **transparent** to the sensor network management applications
- Sysadmins interact with sensor networks using SMP
- Unlike other networks, sensor networks consist of nodes that do not have global identification, and are often infrastructureless
- Therefore, SMP needs to access the nodes by using attribute-based naming and location-based addressing.

## Simple Network Management Protocol (SNMP)
- We cannot use SNMP for a few reasons:
  - Sensor-specific failures are not handled
  - Difficult to find the failed nodes
  - Physical connections are not utilized
  - Commonly, there is not a management agent
  - Specifying nodes is difficult
  - Network is self-configured, so that management server doesn't have all information of sensor nodes.
- There are many challenges associated with SNMP as well:
  - Deployment of nodes and discarding of nodes is not easily handled
  - Requires augmentation to (or new approaches over) traditional network and service management techniques
  - Needs to take into account specific characteristics of WSNs, such as energy waste.

## Management Protocol Requirements
- Fault tolerance
  - **Handle loss of nodes** -> Lack of power, physical damage, environmental interference
- Scalability
  - **Handle high density of nodes** -> The number of sensor nodes is an extreme value of millions
- Production Costs
  - **Make them low cost** -> Cost of a single node is very important to justify the overall cost of the network
- Operating Environment
  - **Survive and maintain communication** -> The bottom of an ocrean, biologically contaminated field, battle field
- Transmission media
  - **Wireless** -> Radio, infrared, optical media
- Hardware constraints
  - **Nodes are tiny** -> Very small size, very light node, limited memory, limited battery
- Power consumption
  - **Limited Tx, computation, lifetime** -> Replenishment of power is impossible
- Changing topology
  - **Nodes** -> Nodes moving, new nodes, loss nodes'

## Functional Areas of Management Protocols

### Fault
- Faults in WSNs are not an exception, and tend to occur frequently, so fault management is a critical function of the management protocol.
- Faults are one major factor that make WSN management different than traditional management.
- The network should be self-diagnostic, meaning that the network monitors itself and finds faulty or unavailable nodes.
- The network should be self-healing, preventing disruptions and acting to recover itself or the node after the self-diagnosis.

### Configuration
- The network should exhibit self-organization, meaning the sensor nodes must be able to organize themselves to form the network
- The network should be self-configuring, the nodes must setup and boot up the network automatically.

### Accounting
- The network should include functions related to the use of resources and corresponding reports
- It establishes metrics, quotas and limits that can be used by functions of other functional areas
- It must provide self-sustaining functionalities.

### Performance
- There is a trade-off to be considered: the higher the number of managed parameters, the higher the energy consumption and thus the lower the network lifetime.
- However, if enough parameter values are not obtained, it may not be possible to manage the network appropriately. 

### Security
- Security functionality for WSNs is intrinsically difficult to be provided, due to their ad-hoc organization, intermittent connectivity, wireless communication and resource limitations.
- A WSN is subject to different safety threats, whether they be internal, external, accidental or malicious.

## Power Management
- Power management refers to the management of a how a sensor node uses its power
- For example, sensor nodes may turn off their receiver after receiving a message from one of their neighbours, which reduces energy consumption and avoids getting duplicated messages.
- When the power level of the sensor node is low, the node may:
  - Broadcast to neighbours that is is low in power
  - Stop participating in message routing
  - Reserce remaining power for sensing

# Messaging Protocols

## Process2Process Communication
- Some examples of process-to-process communication using ports are:
  - **HTTP**: Hyper Text Transfer Protocol
    - Forms the foundation of WWW
    - Follows a request-response model
    - Stateless protocol
  - **CoAP**: Constrained Application Protocol
    - Machine-to-machine (M2M) applications with constrained devices
    - Follows a client-server architecture
  - **WebSocket**
    - Allows full duplex communication over a single socker connection
  - **MQTT**: Message Queue Telemetry Transport
    - Lightweight messaging protocol based on publish-subscribe model
    - Uses client-server architecture
    - Well suited for a constrained environment.
  - **XMPP**: Extensible Message and Presence Protocol
    - Used for realtime communication and stream XML data between network entities.
    - Supports both client-sserver and server-server communication
  - **DDS**: Data Distribution Service
    - Data-centric middleware standards for device-to-device or machine-to-machine communication.
    - Uses a publish-subscribe model
  - **AMQP**: Advanced Message Queuing Protocol
    - Open applicaiton layer protocol for business messaging
    - Supports both point-to-point and publish-subscribe model

## Why not HTTP?
- HTTP has huge packet overhead, mostly consisting of metadata that does not need to be attached to each data payload.
- Because of this, billions of low-power, low-cost IoT devices could not effectively communicate.

## MQTT
- Two of the most promising messaging protocols for small devices are MQTT and CoAP, which are both:
  - Open standards
  - Better suited to constrained environments, compared to HTTP
  - Provide mechanisms for asynchronous communication
  - Run over IP
  - Have a range of implementations.
- MQTT gives flexibility in communication patterns and acts purely as a pipe for binary data, whereas CoAP is designed for interoperability with the web.
- MQTT uses the concept of a message broker, where message brokers handle subscriptions and distribution to interested clients. With this architecture, MQTT is used to funnel sensor readings into a collection point (Broker)
- MQTT specifically targets constrained environments, as it has a small code footprint and limited network bandwidth, allowing it to fit onto embedded devices working within constrained networks.

### MQTT Architecture
- MQTT has a client/server model, where every sensor is a client that connects to the broker (which is just a server) over TCP.
- MQTT is **message-oriented**, meaning that ever message is a discrete chunk of data that can be opaque to the broker.
- Every message gets published to a topic, and clients can subscribe to multiple topics, at which point they receive every message published to their subscribed topics.
- The published-subscriber model allows MQTT clients to communicate one-to-one and one-to-many and many-to-one.

### MQTT Topics
- Each message has a topic, this ensures it decides which message is going to be received by whom.
- Topic is the routing mechanism for MQTT.
- Topics look like file directories, and can use either # as a multi-level wildcard or + as a single level wildcard.
- An example topic could be `cars/44/sensors/#` which if subscribed to would receive all sensor data from car #44. 
- Another example could be `cars/+/sensors/tyres/` which if subscribed to would receive only tyre data from all cars.

### MQTT Messages
- MQTT has 14 message types, which are used to connecct/disconnect, publish, subscribe, maintain connections or ensure QoS.
- Packets consist of a fixed header, optional variable header and optional payload.
  - **Fixed Headers** are present in all MQTT control packets, and it consists of the packet type, the flags and the remaining length
  - **Variable Headers** are present in some MQTT control packets, the content of it varies depending on the packet type.
  - **Payload** is present in some MQTT control packets, and it is the last part of a packet where applicaiton related information is carried.
- The smallest MQTT packet only consists of the fixed header, and has a size of 2 bytes.

### MQTT QoS
- There are 3 levels of QoS for MQTT:
  - **QoS 1: Fire and Forget / At most once**
    - Messages are fired by the client once and no retries are commited.
    - This is the fastest of the three, but message loss may occur.
  - **QoS 2: At least once**
    - Messages are fired until recieved by subscribed clients.
    - This is the second fastest and ensures all data is recieved at least once, but duplication may occur.
  - **QoS 3: Exactly once**
    - Messages are assured to arrive exactly once
    - This is the slowest QoS, but is required for high-rel applications that cannot afford packet loss or duplicaiton.

### MQTT Advantages

#### Scalability
- MQTT's pub/sub model scales well and can be power efficient
- Brokers and nodes publish information and others subscribe according to the message content, type or subject
- Generally, the broker subscribes to all messages (simply `/#`) and then manages information flow to its nodes.

#### Space decoupling
- While the node and broker need to have each other's IP address, nodes can publish info and subscribe to other nodes' published info without any knowledge of each other, as everything goes through the broker.
- This reduces overhead than can accompany TCP sessions and ports, allowing end nodes to operate independently of one another.

#### Time decoupling
- Nodes can publish info regardless of other nodes' states.
- Other nodes can receive the published info from the broker when they are active
- This allows nodes to remain in sleepy states even when other nodes are publishing messages to topics they are subscribed to

#### Synchronization decoupling
- A node that's in the midst of one operation is not interuppted to receive a message published to one of it's subscribed topics.
- The message is queued by the broker until the receiving node is finished with its existing operation
- This reduces repeated operations by avoiding interruptions of ongoing operations or sleepy states.