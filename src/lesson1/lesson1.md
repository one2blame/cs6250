# Lesson 1

This lesson covers internet history, original design choices and principles of
the Internet's architecture. This lesson also covers how these design choices
have shaped the Internet's architecture over time, which resembles an hourglass
figure. Finally, this lesson explores what the Internet could be if we started
over from a clean slate with what we know now. This discussion will cover
example architectural design approaches that optimize for network control,
management and accountability - goals that were not considered when the Internet
was first created.

## Internet Architecture Introduction

This section covers how two hosts running the same application can communicate
despite being located in different types of networks. An example is given where
two BitTorrent clients communicate, one using Ethernet and the other using
WiFi. Because they are using an Application Programming Interface to agree
upon one standard for communication, they both utilize multiple layers of APIs
to transfer data.

An analogy is provided using the airline system, where there are a number of
steps, layers, and functionalities that define how a person can travel from
one location to another using multiple airlines and airplanes.

What are the advantages of having a layered networking stack?

- **Scalability, modularity, and flexibility**

## The OSI Model

This section discusses the
International Organization for Standardization's (ISO)
Open Systems Interconnection (OSI) model, consisting of the following layers:

- Application Layer
- Presentation Layer
- Session Layer
- Transport Layer
- Network Layer
- Data Link Layer
- Physical Layer

While the OSI model has its advantages, what are its disadvantages?

1. Some layers functionality relies upon information from other layers,
violating the goal of layer separation.
2. One layer may duplicate the work of lower layer functionalities - error
recovery can occur in lower layers, but also in higher layers.
3. Additional overhead is incurred by the abstraction of information between
layers.

## Application, Presentation, and Session Layers

Note: in the TCP/IP model of the Internet protocol stack, these three layers are
combined. This is due to the fact that these three layers are so similar and
usually implemented by application developers.

### The Application Layer

Includes some popular protocols:

- HTTP (web content delivery)
- SMTP (e-mail)
- FTP  (file transfer)
- DNS  (domain name resolution)

Packets of information at this layer are referred to as **messages**.

### The Presentation Layer

Plays an intermediate role in formatting the information received from the
Session Layer, and delivers the formatted data to the Application Layer. This
could include something like formatting a video stream or converting bytes from
Big to Little Endian.

### The Session Layer

This layer is responsible for managing the different Transport Layer streams
that belong to the same session between Application processes over a network.
For example, in teleconferencing applications, it ties together the audio and
video streams of a session.

### The Transport Layer

This layer is responsible for the end-to-end communication between two
endpoints. There exist two protocols for the Transport Layer: TCP and UDP.
TCP is a connection-oriented service that guarantees delivery of Application
Layer messages, flow control, and congestion control. UDP is a connection-less
service that doesn't provide any of the previously mentioned features for
Application Layer messages. At this layer, packets of information are referred
to as **segments**.

### The Network Layer

The Network Layer is responsible for routing **datagrams** from one Internet
host to another. At this layer, packets of information are referred to as
**datagrams**. At this layer, the IP protocol is defined, which defines:

- Fields of an IP datagram
- How the source/destination hosts and intermediate routers use fields of a
datagram to ensure the datagram is delivered to the correct host
- Routing protocols to determine the routes that datagrams can take between the
source and destination hosts

### Data Link Layer

At this layer, packets of information are referred to as **frames**. Example
protocols defined in this layer are: Ethernet, PPP, and WiFi. This layer is
responsible for moving frames from one node to the next within a network, not
across. The Data Link Layer offers reliable transmission of **frames** between
two links, however, the reliable delivery service is different than what is
offered at the Transport Layer.

### The Physical Layer

This layer facilities the interaction with the actual hardware that will be
transmitting a frame between two nodes connected through a physical link. The
protocols in this layer depend on the link and transmission medium of the link.
Different Physical Layer protocols are used for Ethernet depending upon if the
transmission medium is twister-pair copper wire, coaxial cable, or fiber optic
cable.

## Encapsulation

Encapsulation is the concept that, as packets of information travel up and down
the network stack, they are correctly encapsulated for that network layer in
order for the packet to be inspected, routed, transmitted, etc. correctly. As
packets of information transfer between each layer of the network stack, they
are encapsulated or de-encapsulated accordingly.

### Intermediate devices

Inspecting the OSI and TCP/IP model and the makeup of intermediate devices,
we can recognize that intermediate devices, routers and switches, usually only
implement layers 1 - 3. This is a design choice, the backbone of the internet
can be less complex and only focus on layers 1 - 3 for routing and transmitting
data. All of the other computationally intensive operations are left up to the
endpoints / hosts at the edge of the network.

## The End to End Principle

The end-to-end (e2e) principle is a design choice that characterized and shaped
significantly the current architecture of the Internet. The e2e principle
suggests that specific application-level functions usually cannot, and
preferably should not be built into the lower levels of the system at the core
of the network.

What were the designers’ original goals that led to the e2e principle?

**Moving functions and services closer to the applications that use them,
increases the flexibility and the autonomy of the application designer to offer
these services to the needs of the specific application.
Thus, the higher-level protocol layers, are more specific to an application.** 

### Violations of the End to End Principle

Some of examples of the E2E principle being violated are firewalls and Network
Address Translation (NAT). Firewalls filter traffic based upon some Access
Control List (ACL), monitoring network traffic and allowing or dropping traffic
based upon it's malicious-ness. Firewalls violate the E2E principle because
they are intermediate devices that are operations between two endpoints
and can drop the communication between said endpoints.

Network Address Translation (NAT) violates the E2E principle, but was designed
as an after-thought because the Internet was due to run out of public IP address
space if too many endpoints were added to the network. NAT violates the E2E
principle because we are using an intermediate device to conduct translation
between two endpoints that would otherwise be unable to communicate - the host
on the private network has a private IP address that is not globally route-able.

## Evolutionary Architecture Model (EvoArch)

Researchers have suggested a model - the Evolutionary Architecture model or
EvoArch - that can help to study layered architectures, and their evolution in a
quantitative manner.

### Implications for the Internet Architecture and its Future

The EvoArch model suggests that the TCP/IP stack was not trying to compete with
the telephone network services. The TCP/IP was mostly used for applications such
as FTP, E-mail, and Telnet, so it managed to grow and increase its value without
competing or being threatened by the telephone network, at that time that it
first appeared. Later it gained even more traction, with numerous and powerful
applications relying on it. The waist of the Internet architecture is narrow,
but also the next higher layer (the transport layer) is also very narrow and
stable. So, the transport layer acts as an “evolutionary shield” for IPv4,
because any new protocols that might appear at the transport layer are unlikely
to survive the competition with TCP and UDP which already have multiple
products. In other words, the stability of the two transport protocols adds to
the stability of IPv4, by eliminating any potential new transport protocols,
that could select a new network layer protocol instead of IPv4.

## Interconnecting Hosts and Networks

Below are descriptions of the devices that offer different services and operate
over different layers:

- **Repeaters and Hubs** - Operate on the physical layer, receive and forward
signals to connect different Ethernet segments, providing connectivity between
hosts that are directly connected. Hosts connected to these devices reside
within the same collision domain, causing them to compete for the same link.
- **Bridges and Layer 2 switches** - Operate on the data link layer based on
MAC addresses. They receive packets and forward them to the appropriate
destination. Limitations include their finite bandwidth, causing them to drop
packets if the buffer space of the bridge or the switch is too full.
- **Routers and Layer 3 switches** - Operate on the network layer, routing
packets between different networks.

### Learning Bridges

A **learning bridge** is a bridge that learns, populates, and maintains a
forwarding table. The bridge consults the table so that it only forwards frames
on specific ports, rather than over all ports. When the learning bridge receives
any frame, it uses this as a "learning opportunity" to learn which hosts are
reachable through which ports. This is because the bridge knows what port a
specific host is communicating over, allowing it to correlate host with port.

## Looping Problem in Bridges and the Spanning Tree Algorithm

In the lectures, a problem is presented in which bridges can infinitely forward
packets if the network is configured in a circular manner. The Spanning Tree
Algorithm works to solve this by having each bridge advertise its NodeID, the
NodeID of the node that it accepts as the root node, and its distance from the
root node. Implementing the Spanning Tree Algorithm, the bridges will coordinate
to eliminate loops in the network, and offending bridges will no longer forward
traffic if they deem they are the cause of the loop.