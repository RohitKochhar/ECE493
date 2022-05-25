# ECE493 Week 4 Part 1: Communication Model, Range Assignment and Topology Control

- [ECE493 Week 4 Part 1: Communication Model, Range Assignment and Topology Control](#ece493-week-4-part-1-communication-model-range-assignment-and-topology-control)
- [Communication Models](#communication-models)
  - [The Wireless Channel](#the-wireless-channel)
  - [Propagation Models](#propagation-models)
    - [The Free Space Propagation Model](#the-free-space-propagation-model)
    - [The Two-Ray Ground Model](#the-two-ray-ground-model)
    - [The Log-Distance Path Model](#the-log-distance-path-model)
- [Transmission Energy Conservation](#transmission-energy-conservation)
- [Topology Control](#topology-control)
  - [Homogenous Critical Transmitting Range(CTR)](#homogenous-critical-transmitting-rangectr)
  - [Non-Homogenous Topology Control](#non-homogenous-topology-control)
  - [Location-Based Topology Control](#location-based-topology-control)
  - [Per-packet and Periodical Topology Control](#per-packet-and-periodical-topology-control)
- [Topology Control in the Protocol Stack](#topology-control-in-the-protocol-stack)

# Communication Models

## The Wireless Channel
- A wireless link between a transmitter and receiver is established if and only if the power of the radio signal received by the receiver is above a certain threshold, called the **sensitivity threshold**.
- We can represent this formally as:
  - There exists a wireless link between *u* and *v* given $P_r \ge \beta$, where:
    - *u*: Transmitter node
    - *v*: Receiver node
    - $P_r$: Power of the signal received by *v*
    - $\beta$: Sensitivity threshold
- The exact value of $\beta$ depends on the features of the wireless transceiver and on the communication data rate.
  - For a given radio, the higher the data rate, the higher the value of $\beta$ implying a stronger requirement on the received power.
  - For simplicity, $\beta$ has the conventional value of 1.
- The received power $P_r$ depends on :
  - The power $P_t$ used by *u* to transmit the radio signal
  - Path loss $PL(u, v)$, which models the radio signal degradation with distance. 

$P_r = \frac{P_t}{PL(u,v)}$

- Thus, the occurance of a radio channel between any two network nodes can be predicted if the path loss model is known.
- The mechanisms that regulate radio signal propagation in the environment can be grouped into 3 categories:
  - **Reflection**
    - Occurs when the EM wave hits the surface of an object that has very large dimensions relative to the wavelength of the propagating signal, like the surface of the earth and large buildings.
  - **Diffraction**
    - Occurs when there are objects with very sharp edges on the radio path between the transmitter and receiver.
  - **Scattering**
    - Occurs when several small objects (relative to the signal wavelength) are between the transmitter and receiver of the radio signal.
    - Typical sources of scaterring are foliage, street signs and more.
- We use the following model to predict radio signal propagation when the path between the transmitter and the receiver is clear and unobstructed (line-of-sight, or LOS, path): 
$P_r(d) = \frac{P_tG_tG_r\lambda^2}{(4\pi)^2d^2L}$, where:
  - $G_t$: Transmiter antenna gain
  - $G_r$: Receiver antenna gain
  - L: System loss factor (not related to propagation)
  - $\lambda$: Wavelength (in meters)
  - *d*: Distance from the transmitter

## Propagation Models

### The Free Space Propagation Model
- Since we don't care about the specific characteristics of the transceiver, we can simplify the above equation to:
$P_r(d) = C_f(\frac{P_t}{d^2})$
  - $C_f$ is a constant that depends on the characteristics of the transceivers.
- This model shows that the received power fall off is proportional to the square of the distance *d* that separates the transmitter and the receiver.
- Combining the power equation with the power sensitivity threshold, we can state that the transmitted message can be correctly received if and only if: $d \le \sqrt{C_fP_t}$
- In other words, the radio coverage of a node transmitting at power $P_t$ is a disk of radius $\sqrt{C_fP_t}$ centered at the node
- The free space equation is valid only for values of *d* that are relatively far from the transmitting antenna.
  - For values of *d* within the so-called close-in distance $d_0$, the path loss can be assumed to be constant
- It is seldom the case that the single direct path between the transmitter and the receiver is the only physical means of propagation of the radio signal.
- For this reason, the free space propagation model is often inaccurate.

### The Two-Ray Ground Model
- The two-ray ground model considers two propagation paths:
  - The direct path between nodes
  - A ground reflected propagation between transmitter and receiver.
- In the two-ray ground propagation model, the received power at a distance *d* is given by: $P_r(d) = P_tG_tG_r\frac{h_t^2h_r^2}{d^4}$, where:
  - $h_t^2$: Transmitter antenna height
  - $h_r^2$: Receiver antenna height
- If the distance between the sender and receiver is relatively large ($d \gt\gt \sqrt{h_th_r}$), the features of the radio transceivers are relatively abstracted, so we can simplify the formula to $P_r(d) = C_t(\frac{P_t}{d^4})$, wehre:
  - $C_t$: A constant that depends on the characteristics of the radio transceivers (t stands for two-ray ground)
- The major difference with the free space model and the two-ray ground model is that the free space model models radio signal falloff proportional to the distance raised to the second power, whereas with the two-ray ground model it is proportional to the fourth power.

### The Log-Distance Path Model
- Combining the simplified two-ray ground model with the sensitivity threshold, we have that the radio coverage region in the two-ray ground model is a disk of radius $\sqrt[4]{C_tP_t}$ centered at the transmitter.
- The log-distance model has been derived combining analytical and empirical methods. Empirical methods are based on field measurements and reverse curve fitting on the experimental data
- This model, which can be seen as a generalization of both the free space and the two-ray ground model, indiciates that the average long-distance path loss is proportional to the separation distance d rasied to a certain exponent $\alpha$, which is called the path loss exponent, or distance-power gradient.
- We can show this formally with: $P_r(d) \propto \frac{P_t}{d^\alpha}$, from which we can see that the radio coverage region in this model is a disk of radius proportional to $\sqrt[\alpha]{P_t}$
- The value of $\alpha$ depends on the environmental conditions, and it has been experimentally evaluated in many scenarios, for example:
  - Free space, $\alpha = 2$
  - Urban area, $\alpha = 2.7 - 3.5$
  - Indoor LOS, $\alpha = 1.6 - 1.8$
  - Indoor no LOS, $\alpha = 4 - 6$

# Transmission Energy Conservation
- The efficient use of the scarce energy resources available to IoT and Sensor Network nodes is one of the fundamental tasks for the network designer.
- Since nodes consume a considerable amount of energy to tx/rx messages, reducing the energy consumed for radio communications is an important issue.
- Suppose node $u$ must send a packet to node $v$, located a distance $d$ away.
  - Node $v$ is within $u$'s transmitting range at maximum power, so direct communication between $u$ and $v$ is possible
  - However, the exists also a node $w$ within the circle of diameter $d$ which intersects both $u$ and $v$.
  - Since $\delta(u, w) = d_1 \lt d, \delta(v, w) = d_2 \lt d$, it is possible to send the packet using $w$ as a relay.
- For this example, we must consider what is the most efficient from the energy-consumption point of view.
  - For simplicity, assume the radio signal propogates according to the free space model, so falloff is proportional to the square of $d$.
  - With these assumptions, the power needed to send the message directly from $u$ to $v$ is proportional to $d^2$.
  - If the packet is related by node $w$, the total power consumption is proportional to $d_1^2 + d_2^2$
  - Through some mathematical derivation, we have $d^2 \ge d_1^2 + d_2^2$. Meaning that it is better to communicate using short, multihop paths between the sender and the receiver.
  - Therefore, instead of using a long, energy-inefficient edge/link, communication can take place along a multihop path composed of short edges/links that connect the two endpoints of the long edge/link.
- The goal of topology control is to identify and 'remove' these energy-inefficient edges from the communication graph.
- The use of a shared communication medium implies that particular care must be paid to avoid that concurrent wireless transmission corrupt each other.
- A typical conflicting scenario occurs when:
  - Node $u$ is transmitting a packet to node $v$ using a certain transmit power $P$
  - At the same time, node $w$ is sending a packet to node $z$ using the same power $P$.
  - $v$ calls within the coverage range of $w$.
  - Since $\delta(v, w) = d_2 \lt \delta(v, u) = d_1$, the power of the interfering signal received by $v$ is higher than that of the intended transmission from $u$, and the reception of the packet sent by $u$ is corrupted.
  - We can ensure correct message reception by increasing the transmit power to a certain value $P^x \gt P$ such that the received power at $v$ is above a certain amount. 
    - This seems to indicate that increasing transmit power is a good choice to avoid packet drops due to interference
    - On the other hand, increasing transmit power at $u$ increases the level of interference experienced by the other nodes in $u$'s surrounding.
    - Therefore, there is a trade-off between the "local view" ($u$ sending a packet to $v$) and the "network view" (reduce the interference level in the whole network)
      - In the former case, a higher transmit power is desirable
      - In the latter case, a lower transmit power is desirable
- From this, we must ask, how should the transmit power be set, if the designer's goal is to maximize the network traffic carrying capacity?
  - In order to answer this, we need to define an appropriate interference model.
  - In this model, the packet transmitted by a certain node $u$ to node $v$ is correctly received if: $\delta(v, w) \ge (1+\eta)\delta(u,v)$, where:
    - $w$: Any other node that is transmitting simultaneously
    - $\eta$: Constant that depends on the features of the wireless transceiver.
  - Therefore, when a certain node is receiving a packet, all the nodes in its interference region must remain silent in order for the packet to be correctly received.
  - The interference region is a circle of radius $(1 + \eta)\delta(u,v)$, centeredat the receiver.
    - In a sense, the area of the interference region measures the amount of wireless medium consumed by a certain communication
    - Since concurrent non-conflicting communications occur only outside each other's interference regionm this is also a measure of the overall network capacity.
- Suppose node $u$ must transmit a packet to node $v$, which is located at a distance $d$.
  - Assume there are intermediate nodes $w_1,\ldots, w_k$ between $u$ and $v$, and that $\delta(u, w_1) = \delta(w_1,w_2) = \ldots = \delta(w_k, v) = \frac{d}{k+1}$
  - From a network capacity point of view, is it preferable to send the packet directly from $u$ to $v$ or to use the multihop path $w_1, w_2, \ldots, v$?
    - To answer this, we must consider the interference ranges in the two scenarios.
      - With **direct transmission**, the interference range of node $v$ is $(1+\eta)d$
      - With **mutlihop transmission**, the interference region for any such transmission is $\pi(\frac{d}{k+1})^2)(1+\eta)^2$
    - By Holder's inequality, we can conclude that, from the network capacity point of view, it is better to communicate using short, multihop paths between the sender and the destination.
  - This observation is another motivating reason for a careful design of the network topology.
    - Instead of using long edges in the communication graph, we can use a multihop path composed of shorter edges that connects the endpoints of the long edge.
    - The goal of topology control techniques is to identify and prune edges that are not power efficient.

# Topology Control
- There are two main cases of topology control
  
## Homogenous Critical Transmitting Range(CTR)
- All the network nodes must use the same transmitting range
- The topology control problem reduces to the simpler problem of determining the minimum value of the radius such that a certain networkwide property is satisfied.
- The value of r is known as the *critical transmitting range (CTR)*, since using a range smaller than r would comprimise the desired networkwide goal.
- By far the simplest formulation of the topology control problem

## Non-Homogenous Topology Control
- Nodes are allowed to choose different transmitting ranges (subject to the condition that the chosen range does not exceed the maximum range)
- Location based, direction based and neighbout based.

## Location-Based Topology Control
- In location based topology control approaches, it is assumed that the most accurate information about node positions is known.
- This information is either used by a centralized authority to compute a set of transmitting range assignments that optimizes a certain measure, or it is exchanges between nodes and used to compute an "almost optimal" topology in a fully distributed manner.
- Typically, location-based approaches assume that the network nodes are location aware.

## Per-packet and Periodical Topology Control
- A final distinction is between per-packet and periodical topology control.
- In the former approach, every node maintains a list of 2 efficient neighbours and for each such neighbout $v$, the transmit power to be used when sending packets to $v$
- Here, the node must be able to know it's neighbours and associate a transmission power with each individual one.
- Therefore, the choice of the transmit power to use is done on a per-packet basis, when the packet is destined to a certain neighbour $v$, the appropriate power $P(v)$ is set, and the packet is transmitted.

# Topology Control in the Protocol Stack
*Pausing at page 26*