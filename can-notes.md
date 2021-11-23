- [1.1. Internet History and Basics](#11-internet-history-and-basics)
  - [History](#history)
  - [Cerf and Kahn's Internetworking Principles](#cerf-and-kahns-internetworking-principles)
  - [Where it comes from](#where-it-comes-from)
  - [Structure of the Internet](#structure-of-the-internet)
- [1.2. Networking and Delays](#12-networking-and-delays)
  - [Definitions](#definitions)
  - [Types and Sources of Delays](#types-and-sources-of-delays)
  - [Calculations](#calculations)
  - [More Definitions](#more-definitions)
- [1.3. Layers of the Internet](#13-layers-of-the-internet)
  - [Internet Protocol Stack Layers](#internet-protocol-stack-layers)
- [1.4. hellofriend.mov - Network Security](#14-hellofriendmov---network-security)
- [2.1. Networking Structure and Protocols](#21-networking-structure-and-protocols)
  - [Definitions](#definitions-1)
  - [TCP & UDP](#tcp--udp)
  - [DNS](#dns)
  - [HTTP](#http)
    - [GET](#get)
    - [POST](#post)
    - [HTTP Delays and Persistency in HTTP](#http-delays-and-persistency-in-http)
  - [IMAP, POP, SMTP](#imap-pop-smtp)
    - [IMAP](#imap)
  - [P2P Networking](#p2p-networking)
  - [BitTorrent](#bittorrent)

# 1.1. Internet History and Basics

## History

I was going to list everything but honestly it's just some military dudes and aloha guys having fun in the 70s connecting everything together and then it gets out of hand, like, big time. If you are curious you can [check out the PPTX yourself](http://gaia.cs.umass.edu/kurose_ross/ppt-8e/Chapter_1_v8.1.pptx).

## Cerf and Kahn's Internetworking Principles

- minimalism, autonomy - no internal changes required to interconnect networks
- best effort service model
- stateless routers
- decentralized control

## Where it comes from

cables, basically.

Internet used to come from telephone cables, this was called DSL. Now it usually comes from TV cables. The telephone/internet or TV/internet signals are transmitted at different frequencies (Frequency Division Multiplexing) which allows them to be carried on the same cable.

## Structure of the Internet

Big (global-sized) networks of ISPs, such as Verizon, AT&T, etc. and large internet companies such as Google, Facebook, etc. are interconnected via IXPs. These big networks, in turn, are connected to regional ISPs, serving a country or some other large region of the globe, such as Kablonet, Türk Telekom etc. and these regional ISPs connect with access ISPs (these might serve cities or districts etc.) which then in turn provide access to end users.

Yani kısaca, Global ISP'ler Local ISP'lere takıyor, Local ISP'ler Access ISP'lere takıyor, Access ISP'ler bize takıyor, bi de Global ISP'ler birbirine takıyor, böylelikle gazeteler için haber niteliği olan bir şey çıkmış oluyor.

IXP: A physical point in the internet where two global-scale ISP networks inter-connect to form a mutualist relationship, which enables each of the ISPs clients to communicate with the other ISP's clients.

# 1.2. Networking and Delays

## Definitions

Routing: Determining the route that a packet should take from its source to its destination. This is done in advance.

Forwarding: The router outputting the incoming packet from its appropriate output port. This is done at the router when the packet arrives at a router.

Store and forward: The entire packet must arrive at a router before it can be transmitted on to the next link.

Packet-switching: All data is divided into small packets and routed through the network piece by piece. This is used on the internet. Good for bursty data.

Circuit-switching: The resources connecting the source and the destination are reserved in advance. The reserved resources stay idle even if they are not actively used. This wastes potential resources. Used in telephony networks.

Network Core: A mesh of interconnected routers which route packets by packet-switching from their source to their destinations.

## Types and Sources of Delays

- Nodal Processing Delay (d<sub>proc</sub>)
  - Delay caused by processing done in the router
  - Check incoming packet for errors
  - Determine correct output for the packet (forwarding)
  - Typically less than milliseconds
- Queueing Delay (d<sub>queue</sub>)
  - Delay caused by waiting at the output buffer (queue) of the router
  - Depends on how congested the router is
- Transmission Delay (d<sub>trans</sub>)
  - Depends on link bandwith/capacity and the length of the packet
  - Time it takes to transmit an entire packet
- Propagation Delay (d<sub>prop</sub>)
  - Time it takes for the bits to travel through the physical medium
  - Depends on the length of the physical link (cable)

Sum of all four of these delays is the total nodal delay (d<sub>nodal</sub>)

We can measure real-world delay experimentally using `traceroute`

## Calculations

Let L be the Length of a packet in bits

Let R be the link bandwith or capacity in bits per second

d<sub>trans</sub> = L/R

---

Let L be the Length of a packet in bits

Let R be the link bandwith or capacity in bits per second

Let a be the average packet arrival rate

then, we can say that:

 L x a / R is the traffic intensity.

if traffic intensity ~= 0 => average queueing delay is small

if traffic intensity ~= 1 => average queueing delay is large

if traffic intensity > 1 => average queueing delay is infinite

---

Let d be the length of the physical link

Let s be the propagation speed which roughly equals 2x10<sup>8</sup> m/s

d<sub>prop</sub> = d/s

## More Definitions

Packet Loss: When a packet arrives to a router with a full output queue, the incoming packet is dropped.

Throughout: Rate of bits transferred between the sender and the receiever, in bits/unit-time

Bottleneck Link: A link on an end-to-end path that limits the total average throughput, because it is the weakest (slowest) link.

# 1.3. Layers of the Internet

## Internet Protocol Stack Layers

- Application (HTTP, FTP, SMTP, etc.)
- Transport (TCP, UDP)
- Network (IPv4, IPv6, ICMP, IPsec, etc.)
- Link (Ethernet, Wi-Fi, etc.)
- Physical (Electronic circuits, bits on the wire)

# 1.4. hellofriend.mov - Network Security

Virus: A **MAL**icious piece of soft**WARE** (malware) that infects by being executed on the victim computer e.g. an email attachment

Worm: Malware that infects passively, and spreads automatically without the victim explicitly executing anything. Worms execute and spread themselves.

Spyware: Malware that spies on you.
- e.g.: Google, Facebook, Microsoft, etc. (<--- joke)

Botnet: A group of lots of infected computers, ready to do a hackers bidding.

Denial of Service: An attack aiming to cripple a node on the internet by hogging necessarry resources, therefore making the target "node" unable to respond to regular traffic.

DDoS: Distributed Denial of Service: A DoS attack but done with the help of a botnet.

Packet sniffing: Listening in on packets sent between two nodes on a network.

Spoofing: Faking, modifying with malicious intent

IP Spoofing: Sending a packet with a false IP address.

# 2.1. Networking Structure and Protocols

## Definitions

Stateful protocol: A protocol that stores state information from previous messages

(Sender-) Push protocol/model: A model in which the sender of a message initiates the connection e.g.: The server sending a client a push notification by saying "This notification is for you, here you go."

(Receiver-) Pull protocol/model: A model in which the receiver of a potential message initiates a connectiion e.g.: Asking the server "Do I have any mail?"

## TCP & UDP

## DNS

Mainly uses UDP, can also use TCP when the response size is larger than 512 bytes.

## HTTP

### GET
Parameters are encoded into the URL, the request body is empty.

Conditional GET: Using If-Modified headers to avoid downloading content if it is cached.

### POST
Parameters are in the request body.

### HTTP Delays and Persistency in HTTP

- Non-persistent HTTP:
  - Open TCP connection (1 Round Trip)
  - At most 1 HTTP request (1 Round Trip)
  - Connection is closed
  - Need to open TCP connection again if I need to do another request.
- Persisten HTTP:
  - Open TCP connection (1 Round Trip)
  - Send as many HTTP requests as you want (n Round Trips)
  - Close the connection when you're done

If I need to do 5 HTTP requests back to back, non-persistent HTTP results in 2+2+2+2+2=10 round trips, while persistent results in only 1+5=6 round trips

## IMAP, POP, SMTP

### IMAP

Used for receiving emails (pull)

Stateful protocol, it stores directory mappings etc.

## P2P Networking

In P2P architecture, both server and client processes are used.

## BitTorrent

Is a hybrid-P2P (hybrid because it uses trackers) protocol, has no RFC because it is proprietery.

Tit-for-tat Mechanism: A user sends chunks to the top 4 peers the user is downloading from with the highest rate.

Optimistic Unchoke: To allow for new peers to enter the swarm, each peer reserves some upload slots to random peers and periodically updates who they are uploading to.