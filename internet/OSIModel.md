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

This model partitions the flow of data in a communication system into seven abstraction layers to describe network communications from the physical implementation of transmitting bits across components to the highest-level representation of data in an application.

Each layer communicates with the adjacent ones by standardized communication protocols & technologies.

| Layer            | Protocol Data Unit (PDU) | Function                                                                                                                                         |
|------------------|--------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|
| 7 - Application  | Data                     | High-level protocols such as for resource sharing or remote file access, e.g. HTTP.                                                              |
| 6 - Presentation | Data                     | Translation of data between a networking service and an application; including character encoding, compression and encryption/decryption.    |
| 5 - Session      | Data                     | Managing communication sessions, i.e., continuous exchange of information in the form of multiple back-and-forth transmissions between two nodes. |
| 4 - Transport    | Segment, Datagram        | Reliable transmission of data segments between points on a network, including segmentation, acknowledgement and multiplexing.                    |
| 3 - Network      | Packet                   | Structuring and managing a multi-node network, including addressing, routing and traffic control.                                                 |
| 2 - Data link    | Frame                    | Transmission of data frames between two nodes connected by a physical layer.                                                                      |
| 1 - Physical     | Bit, Symbol              | Transmission and reception of raw bit streams over a physical medium.                                                                             |

<br>


## 1 - Physical Layer

The physical layer is responsible for the transmission and reception of data between a device, such as a , and a physical transmission medium (cable, optical fiber, printed circuit...).

Devices include routers, network switches, microships.
Transmission mediums includes cables, optical fibers, integrated circuits.

It converts the digital bits into electrical, radio, or optical signals. 
Layer specifications define characteristics such as encoding (voltage, light pulse), voltage levels, the timing of voltage changes, physical data rates, maximum transmission distances, modulation scheme, channel access method and physical connectors. 

This includes the layout of pins, voltages, line impedance, cable specifications, signal timing and frequency for wireless devices.

Physical layer specifications are included in the specifications for the Bluetooth, Ethernet, and USB standards.

For example, a 1 bit might be represented on a copper wire by the transition from a 0-volt to a 5-volt signal, whereas a 0 bit might be represented by the transition from a 5-volt to a 0-volt signal.

<br>


## 2 - Data link Layer

The data link layer provides data transfer between two directly connected nodes. It detects and possibly corrects errors that may occur in the physical layer, defines the protocol to establish and terminate a connection between two physically connected devices and for flow control as well.

The IEEE 802 standard divides the data link layer into two sublayers :

- **Medium access control (MAC) layer** – responsible for controlling how devices in a network gain access to a medium and permission to transmit data.
- **Logical link control (LLC) layer** – responsible for identifying and encapsulating network layer protocols, controls error checking and frame synchronization.

Ex : 

- IEEE 802 networks such as *802.3 Ethernet* or *802.11 Wi-Fi* contain MAC and LLC layers.

- The **Point-to-Point Protocol (PPP)** is a data link layer protocol that can operate over several different physical layers, such as synchronous and asynchronous serial lines.

- The **ITU-T G.hn** standard, which provides high-speed local area networking over existing wires (power lines, phone lines and coaxial cables), includes a complete data link layer that provides both error correction and flow control by means of a selective-repeat sliding-window protocol.

<br>


## 3 - Network Layer

The network layer provides the functional and procedural means of transferring packets from one node to another connected in "different networks".
<br>
A network is a medium to which many nodes can be connected, on which every node has an address and which permits nodes connected to it to transfer messages to other nodes connected to it by merely providing the content of a message and the address of the destination node, and letting the network find the way to deliver the message to the destination node, possibly routing it through intermediate nodes.
<br>
If the message is too large to be transmitted from one node to another on the data link layer between those nodes, the network may implement message delivery by splitting the message into several fragments at one node, sending the fragments independently, and reassembling the fragments at another node.

Message delivery at the network layer is not necessarily guaranteed to be reliable; a network layer protocol may provide reliable message delivery, but *it does not need to do so* (UDP).

<br>


## 4 - Transport Layer

The transport layer provides the functional and procedural means of transferring variable-length data sequences from a source to a destination from one application to another across a network, while maintaining the quality-of-service functions. Transport protocols may be connection-oriented or connectionless.

This may require breaking large protocol data units or long data streams into smaller chunks called **"segments"**, since the network layer imposes a maximum packet size called the **maximum transmission unit (MTU)**, which depends on the *maximum packet size* imposed by all data link layers on the network path between the two hosts. 

The amount of data in a data segment must be small enough to allow for a network-layer header and a transport-layer header. For example, for data being transferred across Ethernet, the MTU is 1500 bytes, the minimum size of a TCP header is 20 bytes, and the minimum size of an IPv4 header is 20 bytes, so the maximum segment size is 1500−(20+20) bytes, or 1460 bytes. 

The process of dividing data into segments is called segmentation; it is an optional function of the transport layer. Some connection-oriented transport protocols - such as TCP - perform segmentation and reassembly of segments on the receiving side; connectionless transport protocols - such as UDP - usually do not.

The transport layer also controls the reliability of a given link between a source and destination host through flow control, error control, and acknowledgments of sequence and existence.
<br>
Some protocols are state and connection-oriented. This means that the transport layer can keep track of the segments and retransmit those that fail delivery through an acknowledgment hand-shake system. The transport layer will also provide the acknowledgement of the successful data transmission and sends the next data if no errors occurred.

Reliability, however, is not a strict requirement within the transport layer. Protocols like UDP, for example, are used in applications that are willing to accept some packet loss, reordering, errors or duplication. 

**Streaming media, real-time multiplayer games and voice over IP (VoIP) are examples of applications in which loss of packets is not usually a fatal problem.**

<br>

The OSI connection-oriented transport protocol defines five classes of connection-mode transport protocols, ranging from class 0 (which is also known as TP0 and provides the fewest features) to class 4 (TP4, designed for less reliable networks, similar to the Internet). 

Class 0 contains no error recovery and was designed for use on network layers that provide error-free connections.
<br>
Class 4 is closest to TCP, although TCP contains functions, such as the graceful close, which OSI assigns to the session layer. Also, all OSI TP connection-mode protocol classes provide expedited data and preservation of record boundaries. 

Detailed characteristics of TP0–4 classes are shown in the following table :

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

The session layer creates the setup, controls the connections, and ends the teardown, between two or more computers, which is called a "session". 

Since DNS and other Name Resolution Protocols operate in this part of the layer, common functions of the session layer include user logon (establishment), name lookup (management), and user logoff (termination) functions. 

Including this matter, authentication protocols are also built into most client software, such as FTP Client and NFS Client for Microsoft Networks.
<br>
Therefore, the session layer establishes, manages and terminates the connections between the local and remote application. The session layer is commonly implemented explicitly in application environments that use remote procedure calls.

<br>


## 6 - Presentation Layer

The presentation layer establishes data formatting and data translation into a format specified by the application layer during the encapsulation of outgoing messages and deencapsulation of incoming messages.

The presentation layer handles protocol conversion, data encryption/decryption, data compression/decompression, incompatibility of data representation between operating systems, and graphic commands. The presentation layer transforms data into the form that the application layer accepts, to be sent across a network.

**Serialization of complex data structures** into flat byte-strings (using mechanisms such as TLV, XML or JSON) can be thought of as the key functionality of the presentation layer.

<br>


## 7 - Application Layer

The application layer is the layer closest to the end user, which means both the OSI application layer and the user interact directly with a software application that implements a component of communication between the client and server, such as File Explorer and Microsoft Word. 

Such application programs fall outside the scope of the OSI model unless they are directly integrated into the application layer through the functions of communication, as is the case with applications such as web browsers and email programs. 

Other examples of software are Microsoft Network Software for File and Printer Sharing and Unix/Linux Network File System Client for access to shared file resources.

Application-layer functions typically include file sharing, message handling, and database access, through the most common protocols at the application layer, such as *HTTP, FTP, SMB/CIFS, TFTP, and SMTP*. 

When identifying communication partners, the application layer determines the identity and availability of communication partners for an application with data to transmit. The most important distinction in the application layer is the distinction between the application-entity and the application. 
<br>
For example, a reservation website might have two application-entities: one using HTTP to communicate with its users, and one for a remote database protocol to record reservations. Neither of these protocols have anything to do with reservations. That logic is in the application itself. The application layer has no means to determine the availability of resources in the network.

<br>

---

### Cross-layer functions

Cross-layer functions are services that are not tied to a given layer, but may affect more than one layer. Some orthogonal aspects, such as management and security, involve all of the layers.