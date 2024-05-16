# The Internet Protocol Suite

### Summary

- [Link Layer](#link-layer)
- [Internet Layer](#internet-layer)
- [Tranport Layer](#tranport-layer)
    - [Transmission Control Protocol (TCP)](#transmission-control-protocol-tcp)
    - [User Datagram Protocol (UDP)](#user-datagram-protocol-udp)
    - [QUIC](#quic)
- [Application Layer](#application-layer)

---

<br>

The **Internet protocol suite**, commonly known as **TCP/IP**, is a framework for organizing the set of communication protocols used in the Internet and similar computer networks according to functional criteria.

Specifies how data should be :
- Packetized.
- Addressed.
- Transmitted.
- Routed. 
- Received.

The foundational protocols in the suite are the **Transmission Control Protocol (TCP)**, the **User Datagram Protocol (UDP)**, and the **Internet Protocol (IP)**.

It is organized into four *abstraction layers*, which classify all related protocols according to each protocol's scope of networking.

**OSI Model**

The TCP/IP model differs from the OSI Model as some layers regroup functions present in different OSI layers.

It does not consider the specifics of formatting and presenting data and <u>does not define additional layers between the application and transport layers</u> as in the OSI model (*presentation and session layers*).
<br>
According to the TCP/IP model, such functions are the realm of libraries and application programming interfaces. 

<br>


## Link Layer

- Corresponding functions in the **Data Link Layer** of the *OSI model*. 
- Lowest level layer of the framework.
- Protocols operate within the host local network.
- Move **packets** between the internet layer interfaces of two different hosts on the *same link*.
- Controlled by the device driver of the network card, firmware, specialized chipsets.

In principle, TCP/IP is designed to be hardware independent and may be implemented on top of virtually any link-layer technology.

This includes not only hardware implementations but also virtual link layers such as **virtual private networks (VPN)** and **networking tunnels**.

The TCP/IP model includes specifications for translating the network addressing methods used in the Internet Protocol to link-layer addresses, such as **media access control (MAC)** addresses.

<br>


## Internet Layer

- Corresponding functions in the **Network Layer** of the *OSI model*.
- Provides functionalities to sends packets across multiple IP networks : internetworking -> **The Internet**.

The Internet requires sending data from the source network to the destination network. This process is called **routing** and is supported by host **addressing** and identification using the hierarchical *IP addressing system*. 

The **<u>Internet Protocol (IP)</u>** is the principal component of the internet layer.
It defines addressing systems to identify and locate hosts on the network :

- **Internet Protocol version 4 (IPv4)** : 32-bit address.
- **Internet Protocol version 6 (IPv6)** : 128-bit address.

IP carries data for a variety of different upper layer protocols. These protocols are each identified by a unique protocol number: for example, **Internet Control Message Protocol (ICMP)** and **Internet Group Management Protocol (IGMP)** are protocols 1 and 2, respectively.

IP does not provide reliability of data transmission.

<br>


## Tranport Layer

- Corresponding functions in the **Transport Layer** of the *OSI model*.
- Provides the functional and procedural means of transferring variable-length data from a source to a destination across a **network**.
- Message transfer services are independent of the underlying network, the structure of data and the logistics of exchanging information.
- Establishes the concept of the **network port** : process-specific transmission channels for applications. By convention, some ports are associated with specific applications & processes.

Connectivity at the transport layer can be categorized as either *connection-oriented*, implemented in **TCP**, or *connectionless*, implemented in **UDP**.


### Transmission Control Protocol (TCP)

Connection-oriented protocol.

Provides **reliability** :

- Data arrives in-order.
- Data has minimal error (i.e., correctness).
- Duplicate data is discarded.
- Lost or discarded packets are resent.
- Includes traffic congestion control.


### User Datagram Protocol (UDP)

Connectionless datagram protocol. Like the IP, it is a best-effort, unreliable protocol. 

Reliability is addressed through error detection using a checksum algorithm.

Typically used for applications such as :

- *Streaming media* (audio, video, Voice over IP, etc.) where on-time arrival is more important than reliability.
- Simple query/response applications like *DNS lookups*, where the overhead of setting up a reliable connection is disproportionately large. 

**Real-time Transport Protocol (RTP)** is a datagram protocol that is used over UDP and is designed for real-time data such as streaming media.


### QUIC

- Emerging new protocol as an alternative transport protocol.
- UDP packets with enhanced transport connectivity relative to TCP. 

**HTTP/3** works exclusively via QUIC.

<br>


## Application layer

- Combination of the 5th (**Session**), 6th (**Presentation**), and 7th (**Application**) Layers of the *OSI model*.
- Includes the protocols used by applications for providing user services or exchanging data over the network connections established by the lower-level protocols.
- May include basic network services such as routing and host configuration.

Examples of application layer protocols :

- **Hypertext Transfer Protocol (HTTP)**.
- **File Transfer Protocol (FTP)**.
- **Simple Mail Transfer Protocol (SMTP)**.
- **Dynamic Host Configuration Protocol (DHCP)**.

Data coded according to application layer protocols are encapsulated into transport layer protocol units (such as **TCP** streams or **UDP** datagrams), which in turn use lower layer protocols to effect actual data transfer.

User protocols vs support protocols :

- Support protocols provide services to a system of network infrastructure. 
- User protocols are used for actual user applications. 

For example, FTP is a user protocol and DNS is a support protocol.