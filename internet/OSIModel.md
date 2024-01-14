# The OSI Model

### Summary

- [1 - Physical Layer](#1---physical-layer)
- [2 - Data link Layer](#2---data-link-layer)
- [3 - Network Layer](#3---network-layer)
- [4 - Transport Layer](#4---transport-layer)
- [5 - Session Layer](#5---session-layer)
- [6 - Presentation Layer](#6---presentation-layer)
- [7 - Application Layer](#7---application-layer)

---

<br>

The **Open Systems Interconnection (OSI)** model is a conceptual model from the *International Organization for Standardization (ISO)*.

- Partitions the flow of data in a communication system into **seven abstraction layers**.
- Those layers describe network communications from the **physical implementation** of transmitting bits across components to the **highest-level representation** of data in an application.

Each layer communicates with the adjacent ones by standardized communication protocols & technologies.

| Layer            | Protocol Data Unit (PDU) | Function                                                                                                                                          |
|------------------|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| 7 - Application  | Data                     | High-level protocols such as for resource sharing or remote file access, e.g. HTTP.                                                               |
| 6 - Presentation | Data                     | Translation of data between a networking service and an application; including character encoding, compression and encryption/decryption.         |
| 5 - Session      | Data                     | Managing communication sessions, i.e., continuous exchange of information in the form of multiple back-and-forth transmissions between two nodes. |
| 4 - Transport    | Segment, Datagram        | Reliable transmission of data segments between points on a network, including segmentation, acknowledgement and multiplexing.                     |
| 3 - Network      | Packet                   | Structuring and managing a multi-node network, including addressing, routing and traffic control.                                                 |
| 2 - Data link    | Frame                    | Transmission of data frames between two nodes connected by a physical layer.                                                                      |
| 1 - Physical     | Bit, Symbol              | Transmission and reception of raw bit streams over a physical medium.                                                                             |

<br>


## 1 - Physical Layer

Transmission and reception of data between a device, and a physical transmission medium.

Devices include routers, network switches, microships.
<br>
Transmission mediums includes cables, optical fibers, integrated circuits.

It converts the digital bits into electrical, radio, or optical signals.
<br>
Layer specifications define characteristics such as encoding (voltage, light pulse), voltage levels, the timing of voltage changes, physical data rates, maximum transmission distances, modulation scheme, channel access method and physical connectors. 

This includes the layout of pins, voltages, line impedance, cable specifications, signal timing and frequency for wireless devices.

Physical layer specifications are included in the specifications for the *Bluetooth*, *Ethernet*, and *USB* standards.

For example, a 1 bit might be represented on a copper wire by the transition from a 0-volt to a 5-volt signal, whereas a 0 bit might be represented by the transition from a 5-volt to a 0-volt signal.

<br>


## 2 - Data link Layer

- Data transfer between two directly connected nodes.
- Detects and possibly corrects errors that may occur in the physical layer.
- Defines the protocol to establish and terminate a connection between two physically connected devices and for flow control.

The IEEE 802 standard divides the data link layer into two sublayers :

- **Medium access control (MAC) layer** – responsible for controlling how devices in a network gain access to a medium and permission to transmit data.
- **Logical link control (LLC) layer** – responsible for identifying and encapsulating network layer protocols, controls error checking and frame synchronization.

Ex : 

- IEEE 802 networks such as *802.3 Ethernet* or *802.11 Wi-Fi* contain MAC and LLC layers.

- The **Point-to-Point Protocol (PPP)** is a data link layer protocol that can operate over several different physical layers, such as synchronous and asynchronous serial lines.

- The **ITU-T G.hn** standard, which provides high-speed local area networking over existing wires (power lines, phone lines and coaxial cables), includes a complete data link layer that provides both error correction and flow control by means of a selective-repeat sliding-window protocol.

<br>


## 3 - Network Layer

Provides the functional and procedural means of transferring packets from one node to another connected in "different networks".

**Network** : 

- Can connect many nodes.
- Each node has an adress.
- Transfer messages by providing content and adress of the destination node.
- Leaves the mean of transportation to the transport layer.

The network layer imposes a maximum packet size called the **maximum transmission unit (MTU)**, which depends on the *maximum packet size* imposed by all data link layers on the network path between the two hosts. 

<br>


## 4 - Transport Layer

Provides the functional and procedural means of transferring variable-length data from a source to a destination across a **network**.

Transport protocols may be connection-oriented or connectionless.


### Segmentation

If the message is too large to be transmitted from one node to another directly via the data link layer between those nodes, the network may implement message delivery by splitting the message into smaller chunks called **"segments"**, sending the fragments independently, and reassembling the fragments at another node.

The amount of data in a data segment must be small enough to allow for a *network-layer header* and a *transport-layer header*.

For example, for data being transferred across **Ethernet**, the MTU is 1500 bytes, the minimum size of a TCP header is 20 bytes, and the minimum size of an IPv4 header is 20 bytes, so the maximum segment size is 1500−(20+20) bytes, or 1460 bytes. 

Segmentation is an optional function of the transport layer. 

Some connection-oriented transport protocols - such as TCP - perform segmentation and reassembly of segments on the receiving side.
<br>
Connectionless transport protocols - such as UDP - usually do not.


### Reliability

Some protocols are **state and connection-oriented** :

- Keep track of the segments and retransmit those that fail delivery through an acknowledgment hand-shake system.
- Provide the acknowledgement of the successful data transmission and sends the next data if no errors occurred.

Message delivery is not necessarily guaranteed to be **reliable**; a transport layer protocol may provide reliable message delivery, but *it does not need to do so* (UDP).

> Streaming media, real-time multiplayer games and voice over IP (VoIP) are examples of applications in which loss of packets is not usually a fatal problem.

---

<br>

The OSI connection-oriented transport protocol defines five classes of connection-mode transport protocols, ranging from class 0 (which is also known as TP0 and provides the fewest features) to class 4 (TP4, designed for less reliable networks, similar to the Internet). 

Class 0 contains no error recovery and was designed for use on network layers that provide error-free connections.
<br>
Class 4 is closest to TCP, although TCP contains functions, such as the graceful close, which OSI assigns to the session layer. Also, all OSI TP connection-mode protocol classes provide expedited data and preservation of record boundaries. 

Detailed characteristics of TP0–4 classes are shown below :

| Feature name                                              | TP0 |	TP1 | TP2 |	TP3 | TP4 |
|-----------------------------------------------------------|-----|-----|-----|-----|-----|
| Connection-oriented network                               |  O  |  O  |  O  |  O  |  O  |
| Connectionless network                                    |  -  |  -  |  -  |	 -  |  O  |
| Concatenation and separation                              |  -  |  O  |  O  |	 O  |  O  |
| Segmentation and reassembly                               |  O  |  O  |  O  |	 O  |  O  |
| Error recovery                                            |  -  |  O  |  O  |	 O  |  O  |
| Reinitiate connectiona                                    |  -  |  O  |  -  |	 O  |  -  |
| Multiplexing / demultiplexing over single virtual circuit |  -  |  -  |  O  |	 O  |  O  |
| Explicit flow control                                     |  -  |  -  |  O  |	 O  |  O  |
| Retransmission on timeout                                 |  -  |  -  |  -  |	 -  |  O  |
| Reliable transport service                                |  -  |  O  |  -  |	 O  |  O  |

<br>

Although not developed under the OSI Reference Model and not strictly conforming to the OSI definition of the transport layer, the **Transmission Control Protocol (TCP)** and the **User Datagram Protocol (UDP)** of the **<u>Internet Protocol Suite</u>** are commonly categorized as layer 4 protocols within OSI.

Transport Layer Security (TLS) does not strictly fit inside the model either. It contains characteristics of the transport and presentation layers.

<br>


## 5 - Session Layer

Setups, establishes, manages and terminates connections between a local and remote application. 

Common functions :

- Login (establishment).
- Name lookup (DNS, Name Resolution Protocols) (management).
- Logout (termination).

Contains **Authentication protocols**.

<br>


## 6 - Presentation Layer

- Data formatting and parsing into a format specified by the application layer during the encapsulation / deencapsulation of messages.

- Handles :
    - Protocol conversion.
    - Data encryption/decryption.
    - Data compression/decompression.
    - Incompatibility of data representation between operating systems.
    - Graphic commands. 

- Transforms data into the form that the application layer accepts, to be sent across a network.

**Serialization of complex data structures** into flat byte-strings (using mechanisms such as TLV, XML or JSON) can be thought of as the key functionality of the presentation layer.

<br>


## 7 - Application Layer

Layer closest to the end user.

Application-layer functions typically include file sharing, message handling, and database access, through the most common protocols at the application layer, such as *HTTP, FTP, SMB/CIFS, TFTP, and SMTP*. 

<br>

---


### Cross-layer functions

Services not tied to a given layer, bu affecting more than one layer. 
<br>
Some orthogonal aspects, such as management and security, involve all of the layers.