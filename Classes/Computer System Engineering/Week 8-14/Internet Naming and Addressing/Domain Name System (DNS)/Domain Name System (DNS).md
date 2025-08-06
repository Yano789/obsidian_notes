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

| Name                                          | Value                                                          | Type  | TTL       |
| --------------------------------------------- | -------------------------------------------------------------- | ----- | --------- |
| Hostname, e.g: sutd.edu.sg                    | IP Address                                                     | A     | N seconds |
| Domain, e.g: sutd.edu.sg                      | The nameserver that is authoritative to this domain            | NS    | N seconds |
| Alias name for some canonical (real) hostname | Real hostname                                                  | CNAME | N seconds |
| Domain, e.g: sutd.edu.sg                      | mailserver name, e.g: sutd-edu-sg.mail.protection.outlook.com. | MX    | N seconds |
**Types:**
- **A**: Address, it contains the IPv4 address of the hostname in question. You might sometimes see type **AAAA** which value contains IPv6 instead of IPv4.
- **NS**: Name Server, it tells which nameservers are authoritative for a that domain in question. You can have multiple NS records for load distribution (increasing availability)
- **CNAME**: Canonical Name, maps an alias name to a true or canonical domain name. Requires more probing (queries) to resolve to an IP eventually. It is like the same website with two or more URLs.
- **MX**: Mail server, points you to the mail server name responsible for the domain in question.

## CNAME Record
The **CNAME** records allow for many-to-one mapping, where multiple domain name points to the same canonical name. For instance, www.twitch.tv and player.twitch.tv both point to twitch.map.fastly.net.

## SOA Record
This type is not covered as part of our syllabus

# Query and Reply Protocol
DNS queries and replies follow a **specific** message format outlined in [RFC 1035](https://datatracker.ietf.org/doc/html/rfc1035), which structures the data to be transmitted over the network.

The format is as follows. Below we explain certain parts of the message:

![[Domain Name System (DNS)-3.png]]

**Identification**: 16 bit number for query, reply uses the same number

**Flags**:
- Query or Reply?
- Recursion desired or available?
- Reply is authoritative?

**Size**: Varies, depending on number of RRs in each section. Generally, replies are larger than queries.

Components of the variable lengths of DNS query / reply:

- **Questions**: name, type fields for a query
- **Answers**: RRs in response to the query
- **Authority**: Records for authoritative servers
- **Additional information**: possibly helpful information

>[!Note]
>Tools like `dig` and `nslookup` are designed to craft DNS query messagse and query DNS servers, then _render_ out the information contained in DNS reply messages. They provide different levels of detail and formats, helping users and administrators understand DNS responses and diagnose network issues.

# Caching
The Local Name Servers will cache hostname-ip mapping once a query is made for a certain *TTL (time to live)*. Due to this caching mechanism, TLD servers are typically cached in DNS local name servers, allowing for faster resolution. On the other hand, Root servers are often not visited.

## Handling Cache Update
Cached entries may be out of date, e.g: if a host changes IP address, it may not be known Internet-wide until all TTLs (time-to-live) expire.

- The authoritative name server decides the DNS record TTL, for example, Netflix’s authoritative name server decides the TTL for its DNS records
- The local nameserver re-queries when TTL expires
- The update or notify mechanisms of these caches are proposed by IETF standard, in particular, [RFC 2136 – Dynamic Updates in the Domain Name System](https://datatracker.ietf.org/doc/html/rfc2136) (DNS UPDATE)

# Record Insertion
>[!Important] Definition
>DNS record insertion refers to the process of adding new records to a DNS zone to manage the resolution of domain names into IP addresses or other information. For example, if you manage your own DNS server at home (authoritative to sites you host at home), then you will need to insert some record (information about your authoritative DNS server at home) to the TLD.
>
> Even though you manage your own DNS zone, it is still part of a larger DNS hierarchy.

Suppose you want your website to be accessible via the internet using your own domain name. You can **insert** (or register) DNS records to ensure that they are recognized Internet-wide, allowing other hosts to find your website. The steps are as follows:

1. Find a DNS Registrar to register the domain name of your site
2. Find authoritative nameservers that will be responsible for solving your domain name
3. Insert DNS records (A type) into the authoritative nameservers
4. Insert DNS records (NS types) of your authoritative nameservers to the TLD

## Registrar
> [!Important] Definition
> A DNS registrar, also known simply as a domain registrar, is a company or organization accredited to manage the reservation of domain names on the internet.

Example registrar: Amazon Domain Registrar, GoDaddy. GoDaddy and AWS Route 53 allows you to register new domain names. You can search for and purchase domain names directly through GoDaddy website or the AWS Route 53 console.’

Note that a registrar is not a registry (see [appendix](https://natalieagus.github.io/50005/ns/07-dns-records-query#registry) for definition of registry). A Registrar interfaces with the general public regarding the registration of their domain names. **In short, they sell domain names**. See more examples of registrars [here](https://www.icann.org/en/accredited-registrars?filter-letter=a&sort-direction=desc&sort-param=name&page=1).

Therefore, suppose for you want your website to be reachable at `examplesite.com`. You then need to **buy** this particular domain name (if it is still available) for any of the registrars above.

## Authoritative Name Servers
You will then **need** to provide the **names** and **IP addresses** of the authoritative name server (primary and secondary server as backup) responsible for resolving this domain name `examplesite.com`.

Authoritative name servers can be maintained by you (if you know how to manage a DNS server), or an ISP or other related companies (DNS hosting providers). For example, SUTD has 3 Authoritative nameservers hosted by starhub, and also SUTD herself.

## TLD Update
Since you rely on AWS Route 53 for your authoritative nameservers, then Amazon is responsible for inserting the NS records for `examplesite.com` into the appropriate TLD server (.com TLD server in this example). These NS records are useful to indicate the Authoritative Name Server responsible for your domain:

- `examplesite.com,` `ns-1312.awsdns-36.org, NS, TTL`
- `examplesite.com,` `ns-788.awsdns-34.net, NS, TTL`

The A record for these two nameservers must also be present and reachable from the internet. For instance, The IP addresses of `ns-1312.awsdns-36.org` and `ns-788.awsdns-34.net` are registered within the respective TLDs (.org and .net). This means that the .org and .net registries contain the `A` records for these nameservers. For example:

- `ns-1312.awsdns-36.org,` `20.50.23.12, A, TTL`
- `ns-788.awsdns-34.net,` `53.25.22.11, A, TTL`

If the authoritative nameserver happen to be in the `.com` domain, then the `.com` TLD should contain glue records to avoid circular dependency. Head to [appendix](https://natalieagus.github.io/50005/ns/07-dns-records-query#glue-records) if you’d like to find out more.

# Attack
Since DNS is a crucial part of the internet, it is prone to various attacks. Example of some DNS attacks are as follows:

- **DDoS attack** (Denial of Service): done either by bombarding root servers with traffic or bombarding TLD servers with traffic. The latter is potentially more dangerous since they are cached by local DNS servers.
    - Root server bombarding is not successful to date due to traffic filtering and that local DNS servers cache IPs of TLD servers, hence we typically bypass the root servers
- **Redirect attack** (Man in the Middle): done via **DNS Cache Poisoning**, which is to send bogus replies to local DNS server, which caches the replies
    - Intercept DNS queries, direct it to a bogus server (not the actual server)
    - Client wont’t be able to reach the actual server
- **Exploit DNS for DDoS**:
    - Send queries with spoofed source address (that’s our target victim IP)
    - Amplify these queries
    - DNS servers that receive queries will answer to our target victim IP and flood it, causing its domain to be inaccessible