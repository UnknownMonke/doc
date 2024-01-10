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

The Internet is an infrastructure, whereas the Web is a service built on top of the infrastructure. It is worth noting there are several other services built on top of the Internet, such as email and IRC.


### Intranet & Extranets

Intranets are private networks that are restricted to members of a particular organization. They are commonly used to provide a portal for members to securely access shared resources, collaborate and communicate.

Extranets are very similar to Intranets, except they open all or part of a private network to allow sharing and collaboration with other organizations. They are typically used to safely and securely share information with clients and stakeholders who work closely with a business. Often their functions are similar to those provided by an intranet: information and file sharing, collaboration tools, discussion boards, etc.

Both intranets and extranets run on the same kind of infrastructure as the Internet, and use the same protocols. They can therefore be accessed by authorized members from different physical locations. 


### Domain Name Service (DNS)

Any Internet-connected computer can be reached through a public IP Address, either an IPv4 address (e.g. 192.0.2.172) or an IPv6 address (e.g., 2001:db8:8b73:0000:0000:8a2e:0370:1337).

The Domain Name System (DNS) is a hierarchical and distributed naming system for computers, services, and other resources in the Internet or other Internet Protocol (IP) networks.

It translates numerical IP addresses needed for locating and identifying computer services and devices to human readable and unique domain names.

**Ownership** :

Domain names cannot be bought. This is so that unused domain names eventually become available to be used again by someone else. If every domain name was bought, the web would quickly fill up with unused domain names that were locked and couldn't be used by anyone.

Instead, you pay for the right to use a domain name for one or more years. You can renew your right, and your renewal has priority over other people's applications. But you never own the domain name.

Companies called registrars use domain name registries to keep track of technical and administrative information connecting you to your domain name.

DNS databases are stored on every DNS server worldwide, and all these servers refer to a few special servers called "authoritative name servers" or "top-level DNS servers".

Whenever your registrar creates or updates any information for a given domain, the information must be refreshed in every DNS database. 
Each DNS server that knows about a given domain stores the information for some time before it is automatically invalidated and then refreshed (the DNS server queries an authoritative server and fetches the updated information from it). Thus, it takes some time for DNS servers that know about this domain name to get the up-to-date information.


### Packets

In networking, a packet is a small segment of a larger message. Data sent over computer networks*, such as the Internet, is divided into packets. These packets are then recombined by the computer or device that receives them.

Suppose Alice is writing a letter to Bob, but Bob's mail slot is only wide enough to accept envelopes the size of a small index card. Instead of writing her letter on normal paper and then trying to stuff it through the mail slot, Alice divides her letter into much shorter sections, each a few words long, and writes these sections out on index cards. She delivers the group of cards to Bob, who puts them in order to read the whole message.

This is similar to how packets work on the Internet. Suppose a user needs to load an image. The image file does not go from a web server to the user's computer in one piece. Instead, it is broken down into packets of data, sent over the wires, cables, and radio waves of the Internet, and then reassembled by the user's computer into the original photo.