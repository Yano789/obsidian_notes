> [!Important] Definition
> 
> The Domain Name System (DNS) is a naming system for computers, services, or other resources connected to the Internet or a network of computers.
> 
> It is a **hierarchical** and **decentralized** naming system that allows computers, services, or resources connected to the Internet or a private network to be identified and accessed. It translates human-friendly domain names, like example.com, into the numerical IP addresses needed by computers to communicate with each other. This system makes browsing the internet and accessing network resources **easier** for users while handling the technical mapping in the background.
> 
> DNS is **both** a naming system and a protocol, read along to find out more.

DNS is a system that acts as a phonebook. We will remember our friends by their names, and not their contact number. When we want to actually contact them, we need to translate their names into their contact numbers using our phonebook. The DNS is much like our phonebook, where it translates between domain name and IP addresses.

# Characteristics

## Distributed Database
The DNS is **implemented** in hierarchy of name servers. We do not centralise DNS because:
- Need to avoid single point of failure,
- Avoid creating a bottleneck traffic volume
- Avoid distant centralized databases, causing long delays for lookups (remember DNS lookup is only name-IP translation! We haven’t even looked up the website yet)
- Need to support ease of maintenance (add/delete/change translation). We do not want to keep going to one place to do this.

**Furthermore, a centralized DNS does not scale.**

## Application Layer Protocol
The Domain Name System (DNS) is vital as one of the core functions of the internet. It enables hosts and name servers to communicate, resolving user-friendly names into numerical IP addresses so computers can locate each other and exchange data. As an application-layer protocol, DNS operates at the top of the Internet Protocol Suite, handling requests from other applications and services to ensure seamless access to network resources.

DNS is implemented at the **network’s edge**, managing complexity through a hierarchical and decentralized system. Key features of this structure include:

- **Hierarchical Organization**: The hierarchical arrangement of root servers, top-level domains, and authoritative name servers ensures efficient and organized domain name resolution.
- **Edge Complexity**: By placing complexity at the network’s edge, DNS remains scalable and effective in handling the growing demands of the internet.

# Services
- **Host aliasing**: map alias names to canonical name
- **Mail server aliasing**
- **Load distribution**: replicated web servers such that many IP addresses correspond to one name

# Structure
DNS is a **distributed** and **hierarchical** database.

![[Domain Name System (DNS).png]]

## Root Server
contacted by local name servers (or end hosts explicitly configured for it) that cannot resolve names. The Root Server does not provide the final answer to the query (i.e., it doesn’t resolve the domain name directly); instead, it directs the query to the appropriate Top-Level Domain (TLD) server (like .com, .org, etc.). There are 13 root servers in the world. Find the list at [](http://root-servers.org/)[http://root-servers.org/](http://root-servers.org/).

The root servers are basically a fixed set of name servers that maintain a list of the authoritative (master/slave) name servers for every registered top level domain (e.g: edu., gov., com., etc). They may be located at:

1. Companies contracted to provide the service by ICANN (The Internet Corporation for Assigned Names and Numbers) or
2. Government institutions.

## Top Level Domain (TLD)
**TLD Server**: responsible for anything after the last dot, such as `.com`, `.edu`, `.sg` etc. They are maintained by **large** organizations or countries. For example, Verisign global registry services is responsible for `.com` domain.

## Authoritative Name Servers
**Authoritative Name Servers**: organization’s own DNS server, providing authoritative (final, no need further query) hostname to IP mappings for organization’s named hosts. They’re maintained by the organization itself or by internet provider / cloud service management system like AWS.

## Local Domain Name Servers
**Local DNS**: also called DNS resolvers are used by DNS clients (our computers or smart devices) to resolve domain names to IP addresses. They serve as proxy for hosts to make DNS queries, and forward queries to the hierarchy:

- Local DNS Name Servers have local cache of recent name-to-address translation pairs
- Need to maintain and update these caches from time to time

Common DNS resolvers include

- ISP-given DNS resolver
- Google DNS resolver: 8.8.8.8
- Cloudflare DNS resolver: 1.1.1.1

# Name Resolution

## Iterative Query
> [!important] Definition
> In an iterative DNS query, the DNS client allows the DNS server to return the _best_ answer it can. If the queried server does not have the answer, instead of asking other servers itself, it returns a referral to other more authoritative DNS servers.

![[Domain Name System (DNS)-1.png]]

> [!Note] DNS Client
> Majority of the “work” (resolution) is done by the DNS client. A DNS client can be any application or tool that initiates DNS queries, such as CLI tools like `dig`, web browsers, OS DNS Resolver, email clients, etc.

## Recursive Query
>[!Important] Definition
>A recursive DNS lookup is where one DNS server communicates with several other DNS servers to hunt down an IP address and return it to the client. The DNS server does **all** the work of fetching the requested information. This is in contrast to an iterative DNS query, where the client communicates _directly_ with each DNS server involved in the lookup.

![[Domain Name System (DNS)-2.png]]

> [!Warning] Potentially Misleading Information
> 
> Note that the diagram above _can_ be slightly misleading (although this is the exact illustration taken from the KR book). It seems to point out that all other DNS servers in the path is doing the work and then answer is _propagated_ back. This might be done for educational purposes. In practice, the root servers and TLD servers do not do the work for us. When a recursive query is made by the DNS client / user, the local DNS server (if it supports recursive query) **will perform iterative** querying to resolve the answer for the user. In the eyes of the user, the Local DNS server that supports recursive query **does all the work**, and hence we regard it as **recursion available**.

# Records
> [!Important] Resource Records
> DNS resource records (RR) are entries stored in a DNS zone file that provide information about a domain. These records are used to facilitate the translation of human-readable domain names into IP addresses (which are necessary for locating and identifying computer services and devices on the Internet) and to provide other essential information associated with the domain.
>
> In short, the DNS is basically a distributed database storing these RRs.

The **data structure** of a resource record is as follows. Each time a client query for hostname resolution, the servers consults these records.

$$
\text{RR = (name, value, type, TTL)}
$$

An RR in general contains the following information (but not limited to): name, value, type, and TTL. The table below explains what each information means:

