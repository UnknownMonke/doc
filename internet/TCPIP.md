# The Internet Protocol Suite

### Summary

- [Link Layer](#link-layer)
- [Internet Layer](#internet-layer)
- [Tranport Layer](#tranport-layer)
    - [Transmission Control Protocol (TCP)](#the-transmission-control-protocol-tcp)
    - [User Datagram Protocol (UDP)](#the-user-datagram-protocol-udp)
- [Application Layer](#application-layer)

---

<br>

The **Internet protocol suite**, commonly known as **TCP/IP**, is a framework for organizing the set of communication protocols used in the Internet and similar computer networks according to functional criteria.
<br>
It provides end-to-end data communication specifying how data should be packetized, addressed, transmitted, routed, and received.

The foundational protocols in the suite are the **Transmission Control Protocol (TCP)**, the **User Datagram Protocol (UDP)**, and the **Internet Protocol (IP)**.

It is organized into four *abstraction layers*, which classify all related protocols according to each protocol's scope of networking.

<br>


## Link Layer

This layer is the lowest component layer of the framework. Protocols operate within the scope of the local network connection to which a host is attached. The size of the link is therefore determined by the networking hardware design. In principle, TCP/IP is designed to be hardware independent and may be implemented on top of virtually any link-layer technology. This includes not only hardware implementations but also virtual link layers such as **virtual private networks** and **networking tunnels**.

The link layer is used to move packets between the internet layer interfaces of two different hosts on the same link. The processes of transmitting and receiving packets on the link can be controlled in the device driver for the network card, as well as in firmware or by specialized chipsets. 

These perform functions, such as framing, to prepare the internet layer packets for transmission, and finally transmit the frames to the physical layer and over a transmission medium. 

The TCP/IP model includes specifications for translating the network addressing methods used in the Internet Protocol to link-layer addresses, such as **media access control (MAC)** addresses.

The link layer in the TCP/IP model has corresponding functions in the **Data Link Layer** of the *OSI model*. 

<br>


## Internet Layer

The Internet requires sending data from the source network to the destination network. This process is called routing and is supported by host addressing and identification using the hierarchical *IP addressing system*. 

The internet layer provides an unreliable datagram transmission facility between hosts located on potentially different IP networks by forwarding datagrams to an appropriate next-hop router for further relaying to its destination. The internet layer has the responsibility of sending packets across potentially multiple networks. With this functionality, the internet layer makes possible internetworking, the interworking of different IP networks, and it essentially establishes the Internet.

The internet layer does not distinguish between the various transport layer protocols. IP carries data for a variety of different upper layer protocols. These protocols are each identified by a unique protocol number: for example, Internet Control Message Protocol (ICMP) and Internet Group Management Protocol (IGMP) are protocols 1 and 2, respectively.

The **<u>Internet Protocol (IP)</u>** is the principal component of the internet layer, and it defines two addressing systems to identify network hosts and to locate them on the network. The original address system of the ARPANET and its successor, the Internet, is **Internet Protocol version 4 (IPv4)**.
<br>
It uses a 32-bit IP address and is therefore capable of identifying approximately four billion hosts. This limitation was eliminated in 1998 by the standardization of **Internet Protocol version 6 (IPv6)** which uses 128-bit addresses. IPv6 production implementations emerged in approximately 2006. 

<br>


## Tranport Layer

The transport layer establishes basic data channels that applications use for task-specific data exchange. The layer establishes host-to-host connectivity in the form of end-to-end message transfer services that are independent of the underlying network and independent of the structure of user data and the logistics of exchanging information. 
Connectivity at the transport layer can be categorized as either connection-oriented, implemented in TCP, or connectionless, implemented in UDP.
<br>
The protocols in this layer may provide error control, segmentation, flow control, congestion control, and application addressing (port numbers).

For the purpose of providing process-specific transmission channels for applications, the layer establishes the concept of the **network port**.

This is a numbered logical construct allocated specifically for each of the communication channels an application needs. For many types of services, these port numbers have been standardized so that client computers may address specific services of a server computer without the involvement of service discovery or directory services.

Because IP provides only a best-effort delivery, some transport-layer protocols offer reliability.

### The Transmission Control Protocol (TCP)

TCP is a connection-oriented protocol that addresses numerous reliability issues in providing a reliable byte stream :

- Data arrives in-order
- Data has minimal error (i.e., correctness)
- Duplicate data is discarded
- Lost or discarded packets are resent
- Includes traffic congestion control

### The User Datagram Protocol (UDP)

UDP is a connectionless datagram protocol. Like the IP, it is a best-effort, unreliable protocol. 

Reliability is addressed through error detection using a checksum algorithm. UDP is typically used for applications such as *streaming media (audio, video, Voice over IP, etc.)* where on-time arrival is more important than reliability, or for simple query/response applications like *DNS lookups*, where the overhead of setting up a reliable connection is disproportionately large. 

Real-time Transport Protocol (RTP) is a datagram protocol that is used over UDP and is designed for real-time data such as streaming media.

<br>

The applications at any given network address are distinguished by their TCP or UDP port. By convention, certain well-known ports are associated with specific applications.

The TCP/IP model's transport or host-to-host layer corresponds roughly to the Transport Layer of the OSI model.

QUIC is rapidly emerging as an alternative transport protocol. Whilst it is technically carried via UDP packets it seeks to offer enhanced transport connectivity relative to TCP. HTTP/3 works exclusively via QUIC.

<br>


## Application layer

The application layer includes the protocols used by most applications for providing user services or exchanging application data over the network connections established by the lower-level protocols. This may include some basic network support services such as routing protocols and host configuration.

Examples of application layer protocols include the **Hypertext Transfer Protocol (HTTP)**, the **File Transfer Protocol (FTP)**, the **Simple Mail Transfer Protocol (SMTP)**, and the **Dynamic Host Configuration Protocol (DHCP)**.

Data coded according to application layer protocols are encapsulated into transport layer protocol units (such as TCP streams or UDP datagrams), which in turn use lower layer protocols to effect actual data transfer.

The TCP/IP model does not consider the specifics of formatting and presenting data and does not define additional layers between the application and transport layers as in the OSI model (presentation and session layers). According to the TCP/IP model, such functions are the realm of libraries and application programming interfaces. 

The application layer in the TCP/IP model is often compared to a combination of the 5th (Session), 6th (Presentation), and 7th (Application) Layers of the OSI model.

At the application layer, the TCP/IP model distinguishes between user protocols and support protocols :

- Support protocols provide services to a system of network infrastructure. 
- User protocols are used for actual user applications. For example, FTP is a user protocol and DNS is a support protocol.