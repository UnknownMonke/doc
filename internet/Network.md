# Network

A network can be defined as a system of lines or channels that cross or interconnect several components.

In the case of computers, networks allow machines to exchange informations, through physical cables (ethernet) or wirelessly (WiFi, Bluetooth).

Networks can be classified in 3 categories :

- **LAN (Local Area Network)** :

    Local network b/w few components to the scale of a house, a school or a company.

- **MAN (Metropolitan Area Network)** :

    City scale, b/w universities buildings for instance. The network itself contains LAN.

- **WAN (Wide Area Network)** :

    Worldwide network, such as the Internet.

<br>

Here is a quick recap of the different communication supports for LAN networks (part of the Physical Layer of the OSI model) :

|                                | Copper wire | Optic cable | WiFi       |
|--------------------------------|-------------|-------------|------------|
| Avg range                      | 100m        | 60km        | 50m        |
| Mobility                       | Avg         | Bad         | Good       |
| Resistance to EM perturbations | Avg         | Very good   | Bad        |
| Data rate                      | Good        | Very good   | Good       |
| Compatibility                  | Good        | Avg         | Good       |
| Security                       | Very good   | Very good   | Avg        |
| Use case                       | Home, Work  | Home, Work  | Home, Work |

<br>

When more than 2 components must communicate together, if each of them is wired with all the others, it can get complicated fast.

<img src="images/network-schema-1.png" alt="drawing" width="400"/>

<br>

To solve this problem, each component on a network is connected to a special component called a **switch**.
<br>
This switch has only one job: like a signaler at a railway station, it makes sure that a message sent from a given component arrives at the right destination component.
<br>
To send a message to component B, component A must send the message to the switch, which in turn forwards the message to component B and makes sure the message is not delivered to component C.

<br>

<img src="images/network-schema-2.png" alt="drawing" width="400"/>

<br>

This structure constitutes a basic LAN network.


### A Network of Networks

What about connecting hundreds, thousands, billions of computers ?
<br>
Of course a single switch can't scale that far, but we can connect 2 switch togethers, and so on, indefinitely.

A switch that connects 2 different networks is called a **router**.

<img src="images/network-schema-3.png" alt="drawing" width="400"/>
<img src="images/network-schema-4.png" alt="drawing" width="400"/>

<br>

Networks can then be represented as **graphs** or **non binary trees**.


## The Internet

Such a network comes very close to what we call the Internet, but how to connect each individual and each home network to one another ?

The specificity of the Internet is that it uses the existing phone network to provide this infrastructure, along with a dedicated underground cable network to convey information between continents.

To connect our network to the telephone infrastructure, we need a special piece of equipment called a **modem**. This modem turns the information from our network into information manageable by the telephone infrastructure and vice versa.

<img src="images/network-schema-5.png" alt="drawing" width="400"/>

<br>

Then, to send messages, we connect to an **Internet Service Provider (ISP)**.

An ISP is a company that manages some special routers that are all linked together and can also access other ISPs' routers. So the message from our network is carried through the network of ISP networks to the destination network. 
<br>
The Internet consists of this whole infrastructure of networks.

<img src="images/network-schema-6.png" alt="drawing" width="200"/>

<br>

Note that in order to connect without using an ISP, one would have to set up a direct link between the source and the destination.

<br>

**Definition** :

The internet is a global network of interconnected networks that communicate using a common set of standards and protocols. These networks are owned and managed by a wide range of organisations, such as national governments, private companies, and academic institutions.


## Communication

Computers connected to the Internet are called **clients** and **servers**.

Clients are the typical web user's internet-connected devices (for example, a computer connected to the WiFi, or a phone connected to a mobile network) and web-accessing software available on those devices (usually a web browser like Firefox or Chrome).

Servers are computers that store webpages, sites, or apps. When a client device wants to access a webpage, a copy of the webpage is downloaded from the server onto the client machine to be displayed in the user's web browser.

Exchange flow :

- The browser goes to the DNS server, and finds the real address of the server that the website lives on.

- The browser sends an HTTP request message to the server, asking it to send a copy of the website to the client.

This message, and all other data sent between the client and the server, is sent across your internet connection using TCP/IP.

- If the server approves the client's request, the server sends the client a "200 OK" message, and then starts sending the website's files to the browser as a series of small chunks called data packets.

- The browser assembles the small chunks into a complete web page and displays it to you (the goods arrive at your door — new shiny stuff, awesome!).


### Internet vs the Web

The Internet is a technical infrastructure which allows billions of computers to be connected all together. Among those computers, some computers (called Web servers) can send messages intelligible to web browsers. 

**Internet** > Infrastructure.

**The Web** > Service built on top of the infrastructure.

There are several other services built on top of the Internet, such as **email** or **IRC**.


### Intranet & Extranets

**Intranets** :

- Private networks.
- Restricted to members of a particular organization.
- Access shared resources, collaborate and communicate.

**Extranets** : 

- Private network partially or totally opened to allow sharing and collaboration with other organizations.
- Safely and securely share information with clients and stakeholders who work closely with a business.
- Similar functions of Intranets.

Both intranets and extranets run on the same kind of infrastructure as the Internet, and use the same protocols. They can therefore be accessed by authorized members from different physical locations. 


### Domain Name Service (DNS)


**Ownership**


### Packets