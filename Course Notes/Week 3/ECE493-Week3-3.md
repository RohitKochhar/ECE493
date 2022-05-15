# Week 3 Part 3: Application Layer and Messaging Protocols (cont.)

- [Week 3 Part 3: Application Layer and Messaging Protocols (cont.)](#week-3-part-3-application-layer-and-messaging-protocols-cont)
- [Messaging Protocols (cont.)](#messaging-protocols-cont)
  - [CoAP (Constrained Application Protocol)](#coap-constrained-application-protocol)
    - [CoAP Resource Discovery](#coap-resource-discovery)
    - [CoAP Method Definitions](#coap-method-definitions)
      - [GET method](#get-method)
      - [POST method](#post-method)
      - [PUT method](#put-method)
      - [DELETE method](#delete-method)
    - [CoAP, a RESTful Protocol](#coap-a-restful-protocol)
    - [CoAP QoS](#coap-qos)
  - [Other Application Layer Protocols](#other-application-layer-protocols)
    - [Advanced Message Queuing Protocol (AMQP)](#advanced-message-queuing-protocol-amqp)
    - [eXtensible Messaging and Presence Protocol (XMPP)](#extensible-messaging-and-presence-protocol-xmpp)

# Messaging Protocols (cont.)

## CoAP (Constrained Application Protocol)
- CoAP is an application layer protocol over UDP (User Datagram Protocol)
- CoAP is an extended tiny version of HTTP
  - Not all HTTP methods are implemented in CoAP
  - CoAP supports some non-HTTP features like push and multicast
  - CoAP is optimized for bandwidth and processing efficiency
- CoAP is RESTful (Representation State Transfer: internet protocol) for easy interfacing with HTTP
- CoAP is designing for datagram transport protocols (UDP instead of TCP)
  - Requests and responses are matched through message tokens
  - Multicast can be used to request responses from various resources
- Designed to used with constrained nodes and lossy networks integration with 6LoWPAN (a wireless extension of the internet protocol)
- CoAP has Built-in resource discovery and observation
- Because CoAP is datagram-based, it may be used on top of SMS and other packet based communications protocols.

### CoAP Resource Discovery
- CoAP defines a standard mechanism for resource discovery.
- Servers provide a list of their resources, along with metadata about them, which is located at the `/.well-known/core`.
- A well-known URI is defined as a default entry-point for requesting links hosted by the server.
- These links are in the application/link-format media type, and allow a client to discover what resources are provided and what media types they are.
- CoAP servers publish CoRE as one way for discovering resources
  - CoRE -> Constrained RESTful Environments Link Format
    - Used as a resource discovery representation for CoAP.
    - Supports filters when discovering resources.

### CoAP Method Definitions

#### GET method
- The GET method retrieves a representation for the information that currently corresponds to the resource identified by the request URI.
- An implementation **may** relax the requirement to answer all retransmissions of a request with the same response, obviating the need to maintain state for message IDs.

#### POST method
- The POST method requests that the representation enclosed in the request be processed. 
- The actual function performed by the POST method is determined by the origin server and dependant on the target resource.
- It usually results in new resource creation or target resource updates.

#### PUT method
- The PUT method requests that the resource identified by the request URI be updated or created with the enclosed representation.
- The representation format is specified by the media type given in the Content-Type Option.

#### DELETE method
- The DELETE method requests that the resource identified by the request URI be deleted.
- In response to a DELETE request, a response should be sent out in case of success or in case the resource did not exist before the request, so it can be handled appropriately.

### CoAP, a RESTful Protocol
- REST (REpresentational State Transfer) is a software architectural style for web client-servers
- Resources are represented as URLs:
  - `example.com/profile/lewis`
  - `example.com/domain/car/44/temp`
- Resources can be retrieved and manipulated using the verbs defined in [CoAP Method Definitions](#coap-method-definitions)

### CoAP QoS
- Requests and response messages can be marked as either "confirmable" or "non-confirmable"
  - Confirmable messages must be acknowledged by the received with an *ack* packet (or a... p*ack*et)
  - Non-confirmable messages must be "fire and forget"
- There are four message types:
  - **Confirmable (CON)**
    - Some messages require an acknowledgement, such messages are called `confirmable`
    - When no packets are lost, each confirmable message elicits exactly one return message of type `acknowledgement` or type `reset`
  - **Non-Confirmable (NON)**
    - Some other messages do not require an acknowledgement, such messages are called `non-confirmable`
    - This is particularly for messages that are repeated regularly as per application requirements, such as repeated readings from a sensor where eventual arrivial is sufficient.
    - `non-confirmable` messages always carry either a request or response, and **must not** be empty.
  - **Acknowledgement (ACK)**
    - An `acknowledgement` message acknowledges that a specific confirmable message, identified by it's message ID, arrived. 
    - It does not indicate success or failure of any encapsulated request.
    - The acknowledgement must echo the message ID of the confirmable message, and must carry a response or be empty.
    - If a server receives a `con` message but was not able to process the request, it will send an empty `ack` in case of client resending this request.
    - `ack` is just to confirm `con` message, no matter if `con` message carries a request or a response.
  - **Reset (3)**
    - A `reset` message indicates that a specific confirmable message was received, but some context is missing to properly process it.
    - This condition is usually caused when the receiving node has rebooted and has forgoten some state that would be required to interpret the message.

## Other Application Layer Protocols

### Advanced Message Queuing Protocol (AMQP)
- Open standard application layer protocol for message-oriented middleware.
- Features include message orientation, queuing, routing (including point-to-point and pub-sub), reliability and security.
- Runs over TCP/IP network protocol that provides ordered, lossless and bidirectional connections.

### eXtensible Messaging and Presence Protocol (XMPP)
- Communications protocol for message-oriented middleware based on XML (eXtensible Markup Language).
- Originally developed for near real-time instant messaging (IM), presence information and contact list maintenance.
- Designed to be extensible, the protocol has been used also for pub-sub systems, signaling for VoIP, video, file transfer, gaming and IoT applications.
- Many XMPP features make it a preferred protocol for many IM applications and relevant within the scope of the IoT.
- XMPP is secure and allows for the addition of new applications on top of the core protocols.
- Runs over TCP/IP network protocol that provides ordered, lossless and bidirectional connections. (Just like AMQP)