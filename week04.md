# Internet Security I
Date: 20200226

## Internet Security
Protocols
How to translate name to address: DNS
How to reach address? TCP
How to talk securely? SSL/TLS

Desired properties

## BGP
Inter domain
Autonomous system (AS)

AS --> AS number (ASN)

IP Address blocks are assigned to Ases

Revisit subnet

192.0.0.0/24. The first 3 octets is network section. Last 8 bit is host section.

Route origination
Border routers anounce prefixees

AS: peerings

## S-BGP
Secure origin BGP (soBGP)
Interdomain route validation

S-BGP
Use PKI
Use certificate to authenticate AS

Challenges:
New infrastructure is required
NOC
Regional registry
Certificate repositry

That makes S-BGP not widely deployed
Too comples for Ases
Expesinve computation memory

## DNS
Secure origin BGP (soBGP)
Interdomain route validation

S-BGP
Use PKI
Use certificate to authenticate AS

Challenges:
New infrastructure is required
NOC
Regional registry
Certificate repositry

That makes S-BGP not widely deployed
Too comples for Ases
Expesinve computation memory

## DNS
Hierarchy
ICANN
Resource records
UDP by default, fallback to TCP for larger responses

Domain zone:
Org zone
Wikipedia.org zone
www.wikipedia.org zone
Revisit CN materials

2 approach of DNS
Recursive and non recursive


## DNS Caching

## DNS Security
No security properties
On path adversary
	• Manipulate DNS responses
Off path adversary
	• Kaminsky DNS vulnerability

## Kaminsky’s Attack
* Client request DNS resolve to recurisve name servert
* Adversary slow down the recursive call
* At the same time adversary try to guess the src port and match the request id to give fake response to the client
* Client get the response from the recursive NS afake IP address which come from adversary 
* Client unknowingly open connection to the fake IP address assuming that is the legitimate destiation

## DNS Security Extension (DNSSEC)
PKI
New RRs: RRSIG, DNSKEY, DS

DNSSEC:
Now widely deployed
Increases amplification factor
Not enough value proposition

## TLS
* Domain validated (DV)
* Organization-Validate (OV): not popular
* Extended-Validated(EV) Certificate: abandoned

DANE
DNS based .…

CAA

## Readings
* [SoK: SSL and HTTPS: Revisiting Past Challenges and Evaluating Certificate Trust Model Enhancements](https://pdfs.semanticscholar.org/1331/5d952a43c391bf4910271fc2582858e86e9e.pdf)
* [Security vulnerabilities in DNS and DNSSEC](https://pdfs.semanticscholar.org/fbb5/70fd509305d0bec9679bff16ea33630733fb.pdf)
* [A Survey of BGP Security Issues and Solutions] (https://www.researchgate.net/profile/Jennifer_Rexford/publication/224092573_A_Survey_of_BGP_Security_Issues_and_Solutions/links/00b7d525f3efdb03af000000.pdf)
