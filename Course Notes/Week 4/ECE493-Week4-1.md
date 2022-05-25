# ECE493 Week 4 Part 1: Communication Model, Range Assignment and Topology Control

- [ECE493 Week 4 Part 1: Communication Model, Range Assignment and Topology Control](#ece493-week-4-part-1-communication-model-range-assignment-and-topology-control)
- [Communication Models](#communication-models)
  - [The Wireless Channel](#the-wireless-channel)
  - [Propagation Models](#propagation-models)
    - [The Free Space Propagation Model](#the-free-space-propagation-model)
    - [The Two-Ray Ground Model](#the-two-ray-ground-model)
    - [The Log-Distance Path Model](#the-log-distance-path-model)
- [Topology Control and Energy Conservation](#topology-control-and-energy-conservation)

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

# Topology Control and Energy Conservation
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

*Pausing at page 15*
