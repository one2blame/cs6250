# Lesson 2

This lecture covers the transport layer and mainly focuses on the TCP protocol.

## Introduction to the Transport Layer

This layer provides and end-to-end connection between two applications that
are running on different hosts. The transport layer provides this logical
connection regardless if the hosts are in the same network.

* Messages at the transport layer are called **segments**.
* The transport layer provides functionalities like data transfer integrity,
flow control, transmission control, etc. - things the Network Layer is unable
to provide.

There are two main protocols:

* **Transmission Control Protocol (TCP)** - connection-oriented protocol.
Provides reliable transmission, transmission control, flow control, and
congestion control.
* **User Datagram Protocol (UDP)** - connection-less protocol. Provides no
congestion control, connection management, or similar overhead / mechanisms.
Useful for real-time applications that are sensitive to delays. Packet structure
is as follows:
  * Source and destination ports.
  * Length of the segment.
  * Checksum.

### Multiplexing and Demultiplexing

Enabled by the use of **ports** at the Transport Layer - used to multiplex
multiple connections for a host. A combination of IP address and Port Number
consititutes a **socket**.

* **Multiplexing** - the encapsulation of data into segments with header
information identifying the sender and receiver of a segment.
* **Demultiplexing** - the unpacking of a segment and interpretation of a header
in order to deliver the data to its respective application.

## Goals for congestion control

* **Efficiency** - throughput and utilization of the network should be as high
as possible.
* **Fairness** - each device should get a fair share of the network bandwitdth.
* **Low delay** - ensuring applications sensitive to delays receive necessary
data as quickly as possible.
* **Fast convergence** - flow should be able to converge to fair allocation
quickly.

## End-to-end vs network-assisted congestion control

**End-to-end** congestion control involves the hosts communicating and using the
same protocols in order to control the congestion on the network. This is
currently implemented with TCP.

**Network-assisted** congestion control involves network devices such as core
routers implementing congestion control, which does not follow the end-to-end
design of the Internet that is currently adopted. This design would require
core routers to have much more computing power.

### How do hosts detect congestion?

Hosts detecting congestion through packet delay and packet loss. The indicators
can both be detected by TCP via a check of round-trip time and a loss of
segments for each transmission window.

## Definitions

* **flow control** - controlling the transmission rate to proctect the
receiver's buffer.
* **congestion control** - controlling the transmission rate to protect the
network from congestion.
