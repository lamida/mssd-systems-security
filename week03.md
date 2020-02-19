# Network Security
Date: 202001219

Network is set of interconnected computers that share resources.

Internet is network of networks.

Network is modeled in layers. Theoritical presentation often uses OSI Layers:
* Application
* Presentation
* Session
* Transport
* Network
* Data Link
* Physical
The layers above numbered from 7 to 1.

Teh alternative layer is TCP/IP layers:
* Application
* Transport
* Network
* Link
* Physical

Layer model is an abstraction how each of layer handle different responsibilites. A message will be created in application layer, then passed one by one layer to the bottom layer which then is sent to the destination in its bottom layer and buble up to the application layer in that destination. Each layer will encapsulate additional envelopes or metadata in the sender side. In the recepient, each layer will deencapsulate each of the envelopes and metadata.

# Layer 1: Physical
* Usually is implemented in a physical chip
* Varies depends on the systems
* Operates on raw bits
* Encoding, decoding, transmission, signaling

## Layer 1 Attacks
* Physical attack. E.g. shark bytes google undersea cable.
* Jamming
* Eavesdropping

# Layer 2: Data Link
* In the past: PPP, SLIP, MPLS, ATM
* Now mainly Ethernet:
    * Simple
    * Frames as data units
    * Hubs (dumb) and switches (smart, switch table)

## Layer 2 Attacks
* Hubs and switches Content Addressable Memory (CAM) overflow. Flood hubs and switches tables.
* ARP sniffing and spoofing. Spoof mac address in hubs. MiTM!
* VLAN attacks
* MAC Spoofing
* DHCP attacks

## Layer 2 Attacks Prevention
* Port Security
* MACsec: expensive operations

## Wifi Security
* Wifi is open medium. Anyone can connect without the need of physical connection.
* WEP
* WPA
* WPA2
TODO: Summary above
TODO: read about 802.1X

# Layer 3: Network
* IP. Addressing. IPv4 (32 bit address). IPv6 (128 bit address). Some changes in the message structure too.
* IP is connectionless
* Routing protocols

## Layer 3 Attacks
* Doesn't need to be collocated physically
* DDoS
* IP Spoofing. You can just change source address of your IP packet. Nobody will validate.
* Smurf Attack
* Routing attacks
* Eavesdropping, modification, injection

## Smurf attack
Attacker will create ICMP request using spoofed source address to a broadcast address. Now all node in the network will receive the ICMP message and reply to the spoofed address. The spoofed address will be flooded by the ICMP reply it never sent.

## Layer 3 Attacks Prevention
* Disable broadcast address
* Secure routing protocols
* IPSec. TODO: read more about it.

# Layer 4: Transport
* Segment is the data unit
* TCP: reliable, handshake, sequence number
* UDP: fire and forget, connectionless, no frills

## Layer 4 Attacks
* DDoS
* UDP Spoofing
* TCP Hijacking. TODO: what is this?
* Connection reset and slowdown
* SYN flooding. Fix: SYN cookies, don't initiate connection before SYN-ACK.
* DNS Attack

## SYN Cookies
TCP handshake initiates with sender sends SYN message with seq=x. Recipient will generate y number from the message using hash of e.g. IP address and port of the sender plus some other information. Server then sends SYN-ACK back to the sender with seq=y and ack=x+1. Sender sends back seq=x+1 and ack=y+1. Server can check the ack to makesure the hash matches.

## Layer 4 Attacks Prevention
* Random source port and sequence numbers
* SYN Cookies
* Cryptography
    * TCPCrypt: TODO read about this
    * TLS/SSH (this is in between transport and application layer)


# Other Defenses and Mechanisms
* Management: update periodically
* Filtering: use firewall
* Intrusion Detection
* Data Protection: Encryption and Authentication

## Firewalls
* Network and host based
* Packet filters (1st gen)
* Stateful filters (2nd gen)
* Application layer (3rd gen)

## Intrusion Detection
TODO

# Reading
* Anderson Chapter 21
* [A Look Back at “Security Problems in the TCP/IP Protocol Suite”](https://www.cs.columbia.edu/~smb/papers/acsac-ipext.pdf)


