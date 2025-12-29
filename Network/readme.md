## Networking Fundamentals to Learn (Self-Study)

Even before taking paid courses, you should master these basics:

1 what is a computer metwork how to internet work

2 OSI & TCP/IP models

3 IP Addressing & Subnetting

4 DNS & Routing

5 Ports & Protocols (TCP/UDP)

6 Firewalls & Security Groups

7 Network Tools: ping, traceroute, netstat, tcpdump, nmap

8 Linux Networking (ip, ifconfig, route)

9 Cloud Networking (VPCs, subnets, gateways)

10 Container/Kubernetes networking (CNI plugins, overlay networks)  |

---

## 1 what is a computer metwork how to internet work

A computer network is a group of two or more computers/devices connected together
so they can share data, resources, and services.
👉 A computer network allows devices to communicate with each other

Main Components of a Network:

Computer / Mobile / Server
Router (connects networks)
Switch (connects devices)
Modem (connects to ISP)
Cables / Wi-Fi
IP Address (unique identity)

Types of Computer Networks

| Type | Full Form                 | Example             |
| ---- | ------------------------- | ------------------- |
| LAN  | Local Area Network        | Home / Office Wi-Fi |
| MAN  | Metropolitan Area Network | City-wide network   |
| WAN  | Wide Area Network         | Internet            |
| PAN  | Personal Area Network     | Bluetooth, hotspot  |

Step-by-Step: How Internet Works
1️⃣ You type a website name
Example: [www.google.com](http://www.google.com)

2️⃣ DNS converts name to IP address
DNS = Domain Name System
Converts google.com → 142.250.190.14
👉 Computers communicate using IP addresses, not names.

3️⃣ Request goes to your ISP
ISP = Internet Service Provider
Example: Jio, Airtel, BSNL
Your ISP forwards your request to the correct server.

4️⃣ Data travels through routers
Routers decide best path for data
Data is broken into packets

5️⃣ Server sends response back
Google server sends webpage data
Packets travel back through the network

6️⃣ Browser displays website
Your browser (Chrome, Edge, Firefox) shows the page.
Common Internet Protocols
HTTP / HTTPS – Web browsing
TCP/IP – Data transmission
FTP – File transfer
SMTP – Email sending
DNS – Name resolution

Key Internet Components

| Component  | Role                      |
| ---------- | ------------------------- |
| Client     | Your computer / mobile    |
| Server     | Stores website data       |
| ISP        | Provides internet access  |
| Router     | Directs data traffic      |
| DNS        | Converts domain → IP      |
| IP Address | Unique identity of device |
| Protocols  | Rules for communication   |

---

## 2 OSI & TCP/IP models

📘 What is OSI Model?

OSI (Open Systems Interconnection) is a conceptual model that explains how data travels from one computer to another in 7 layers.

🧱 OSI Model – 7 Layers (Top → Bottom)

| Layer No | Layer Name       | What it does       | Example        |
| -------- | ---------------- | ------------------ | -------------- |
| 7        | **Application**  | User interaction   | Browser, FTP   |
| 6        | **Presentation** | Format, encryption | SSL, JPEG      |
| 5        | **Session**      | Session management | Login sessions |
| 4        | **Transport**    | Reliable delivery  | TCP / UDP      |
| 3        | **Network**      | Routing, IP        | Router, IP     |
| 2        | **Data Link**    | MAC address        | Switch         |
| 1        | **Physical**     | Cables, signals    | Ethernet       |

📌 Real Example (Opening a Website)

Application → Browser sends request
Presentation → Data encrypted
Session → Session established
Transport → TCP splits data
Network → IP routing
Data Link → MAC addressing
Physical → Electrical signals sent

---

🔶 TCP/IP Model (4 Layers)

📘 What is TCP/IP Model?
TCP/IP is the practical model used in the real internet.

🧱 TCP/IP Model – 4 Layers

| TCP/IP Layer   | What it includes | OSI Mapping |
| -------------- | ---------------- | ----------- |
| Application    | HTTP, FTP, DNS   | OSI 7,6,5   |
| Transport      | TCP, UDP         | OSI 4       |
| Internet       | IP, ICMP         | OSI 3       |
| Network Access | Ethernet, Wi-Fi  | OSI 2,1     |

Data Flow (Simple)

Sender
↓
Application
↓
Transport (TCP/UDP)
↓
Internet (IP)
↓
Network Access
↓
Internet
↓
Receiver

🧪 Protocols You MUST Remember
Application Layer
HTTP / HTTPS
FTP
SMTP
DNS
SSH

Transport Layer
TCP (Reliable)
UDP (Fast)

Internet Layer
IP
ICMP

Network Layer
Ethernet
Wi-Fi

---

## 3  IP Addressing & Subnetting

🔢 What is an IP Address?
An IP Address (Internet Protocol Address) is a unique number given to every device on a network.

👉 Just like your home address, an IP address identifies:

📌 What is IP Class?
IP classes divide IPv4 addresses into fixed ranges based on network size.
This is called Classful Addressing (old method).

👉 Today we mostly use CIDR, but IP classes are important for basics & interviews.

🧱 IP Address Classes (A to E)

| Class | Range                       | Default Mask | Networks | Hosts per Network | Usage          |
| ----- | --------------------------- | ------------ | -------- | ----------------- | -------------- |
| **A** | 1.0.0.0 – 126.255.255.255   | /8           | Very few | Very large        | ISPs, big orgs |
| **B** | 128.0.0.0 – 191.255.255.255 | /16          | Medium   | Medium            | Universities   |
| **C** | 192.0.0.0 – 223.255.255.255 | /24          | Many     | Small             | Small networks |
| **D** | 224.0.0.0 – 239.255.255.255 | N/A          | N/A      | N/A               | Multicast      |
| **E** | 240.0.0.0 – 255.255.255.255 | N/A          | N/A      | N/A               | Reserved       |

🧱 Types of IP Addresses
1️⃣ IPv4
32-bit address
Written in 4 numbers (0–255)
Example:10.10.101.10

2️⃣ IPv6
128-bit address
Created due to IPv4 shortage
Example:2001:0db8:85a3::8a2e:0370:7334

---

🧮 What is Subnetting?
Subnetting means dividing one big network into smaller networks.

👉 Why?
Better security
Less traffic
Easy management
Cloud networking (VPCs)

🎭 Subnet Mask (MOST IMPORTANT)

Subnet mask tells:
Network part
Host part

Common Subnet Masks

| CIDR | Subnet Mask     | Hosts |
| ---- | --------------- | ----- |
| /24  | 255.255.255.0   | 254   |
| /25  | 255.255.255.128 | 126   |
| /26  | 255.255.255.192 | 62    |
| /27  | 255.255.255.224 | 30    |
| /28  | 255.255.255.240 | 14    |

🚦 Network IP & Broadcast IP
Network IP → First IP (cannot assign)
Broadcast IP → Last IP (cannot assign)

ex  192.168.1.0 → Network
192.168.1.255 → Broadcast

✅ CIDR Basic Examples

🔹 Example: /26
192.168.1.0/26

Host bits: 6
Total IPs: 64
Usable IPs: 62

🚀 Quick CIDR Cheat Sheet

| CIDR | Total IPs | Usable |
| ---- | --------- | ------ |
| /30  | 4         | 2      |
| /29  | 8         | 6      |
| /28  | 16        | 14     |
| /27  | 32        | 30     |
| /26  | 64        | 62     |
| /25  | 128       | 126    |
| /24  | 256       | 254    |
| /16  | 65,536    | 65,534 |

---

## 4🌍 DNS & Routing (Networking Basics for DevOps)

1️⃣ DNS (Domain Name System)
🔹 What is DNS?
DNS converts a domain name (human-friendly) into an IP address (machine-friendly).
👉 Computers understand IP, not names.

🔄 How DNS Works (Step-by-Step)
1️⃣ You type [www.example.com](http://www.example.com)
2️⃣ Browser checks local cache
3️⃣ If not found → asks DNS Resolver (ISP)
4️⃣ Resolver asks:
Root DNS Server
TLD Server (.com)
Authoritative DNS Server
5️⃣ IP address is returned
6️⃣ Browser connects to server using IP

🧾 Common DNS Record Types

| Record    | Purpose       | Example               |
| --------- | ------------- | --------------------- |
| **A**     | Domain → IPv4 | example.com → 1.2.3.4 |
| **AAAA**  | Domain → IPv6 | example.com → ::1     |
| **CNAME** | Alias         | www → example.com     |
| **MX**    | Mail server   | Gmail                 |
| **NS**    | Name servers  | AWS Route 53          |
| **TXT**   | Verification  | SPF, DKIM             |

🧑‍💻 DNS in DevOps (Real Use)

Load balancers (Round-robin DNS)
Blue-Green deployments
Failover & health checks
Kubernetes services
Cloud DNS (Route 53)

---

🔹 What is Routing?

Routing decides how data packets travel from source to destination across networks.
👉 Routers read IP addresses and forward packets.

🛣️ How Routing Works
1️⃣ Packet leaves source
2️⃣ Router checks Routing Table
3️⃣ Chooses best path
4️⃣ Forwards packet
5️⃣ Reaches destination

Routing Table (Simple)

| Destination    | Gateway     | Interface |
| -------------- | ----------- | --------- |
| 192.168.1.0/24 | local       | eth0      |
| 0.0.0.0/0      | 192.168.1.1 | eth0      |

Types of Routing

| Type            | Description           |
| --------------- | --------------------- |
| Static Routing  | Manual routes         |
| Dynamic Routing | Automatic (OSPF, BGP) |
| Default Routing | Catch-all route       |

DNS vs Routing (Difference)

| DNS                | Routing           |
| ------------------ | ----------------- |
| Converts name → IP | Moves packets     |
| Happens first      | Happens after     |
| Uses domain names  | Uses IP addresses |

---

## 6 Firewalls & Security Groups

🧱 What is a Firewall?

A firewall is a security system that allows or blocks network traffic based on rules.
👉 It protects systems from unauthorized access.

🔹 Simple definition

Firewall = Gatekeeper of your network

🚦 What Does a Firewall Control?

Firewalls filter traffic based on:
IP address
Port number
Protocol (TCP/UDP)
Direction (Inbound / Outbound)

🔄 Types of Firewalls

| Type                | Description            | Example           |
| ------------------- | ---------------------- | ----------------- |
| Network Firewall    | Protects whole network | Router firewall   |
| Host-based Firewall | Protects one machine   | `iptables`, `ufw` |
| Cloud Firewall      | Managed by cloud       | AWS SG, NACL      |

---

☁️ What is a Security Group? (AWS)

A Security Group is a virtual firewall used in Amazon Web Services (AWS) to control traffic at the instance level.📥 Inbound and Outbound Rules
👉 Applied to:

EC2
Load Balancer
RDS
EKS nodes

🧠 Real AWS Security Group Example Inbound and Outbound Rules

| Type  | Port | Source    |
| ----- | ---- | --------- |
| HTTP  | 80   | 0.0.0.0/0 |
| HTTPS | 443  | 0.0.0.0/0 |
| SSH   | 22   | My IP     |

Security Group vs Firewall (Linux)

| Feature        | Security Group | Linux Firewall     |
| -------------- | -------------- | ------------------ |
| Level          | Cloud instance | OS level           |
| Stateful       | ✅ Yes          | ❌Usually stateless |
| Rules          | Allow only     | Allow & Deny       |
| Used in DevOps | ✅ Daily        | ✅ Daily            |

Security Group vs NACL (Important)

| Feature       | Security Group | NACL         |
| ------------- | -------------- | ------------ |
| Level         | Instance       | Subnet       |
| Stateful      | ✅ Yes          | ❌ No         |
| Rules         | Allow only     | Allow & Deny |
| Order matters | ❌ No           | ✅ Yes        |

---

## 7 Network Tools: ping, traceroute, netstat, tcpdump, nmap

🔍 Complete Network Tools Comparison Table

| Tool           | Purpose           | What it Checks        | Common Use           | DevOps Use Case     |
| -------------- | ----------------- | --------------------- | -------------------- | ------------------- |
| **ping**       | Test connectivity | Host reachable or not | Check server up/down | Health check        |
| **traceroute** | Path tracking     | Network hops          | Find delay/failure   | Debug latency       |
| **netstat**    | Connection status | Ports & services      | Check open ports     | App troubleshooting |
| **tcpdump**    | Packet capture    | Live traffic          | Deep debugging       | Security & issues   |
| **nmap**       | Network scanning  | Open ports/services   | Security scan        | Infra audit         |

---

🟢 `ping` Command

| Item       | Details                       |
| ---------- | ----------------------------- |
| Function   | Checks if a host is reachable |
| Protocol   | ICMP                          |
| Output     | Time, packet loss             |
| Layer      | Network (L3)                  |
| Limitation | Firewall may block ICMP       |

Syntax

```bash
ping google.com
ping -c 4 8.8.8.8
```

Use Case

* Server is **UP or DOWN**
* Basic connectivity test

---

🟡 `traceroute` / `tracert`

| Item     | Details           |
| -------- | ----------------- |
| Function | Shows path (hops) |
| Protocol | ICMP / UDP        |
| Output   | Each router hop   |
| Layer    | Network (L3)      |
| Windows  | `tracert`         |
| Linux    | `traceroute`      |

Syntax

```bash
traceroute google.com
tracert google.com
```

Use Case

* Find **where network breaks**
* Debug slow response

---

🔵 `netstat`

| Item        | Details           |
| ----------- | ----------------- |
| Function    | Shows connections |
| Shows       | Ports, services   |
| Layer       | Transport (L4)    |
| Status      | Old but common    |
| Alternative | `ss`              |

Syntax

```bash
netstat -tulnp
netstat -an
```

Common Flags

| Flag | Meaning   |
| ---- | --------- |
| `-t` | TCP       |
| `-u` | UDP       |
| `-l` | Listening |
| `-n` | Numeric   |
| `-p` | Process   |

Use Case

* Check if app is listening on port
* Find port conflicts

---

🔴 `tcpdump`

| Item     | Details         |
| -------- | --------------- |
| Function | Capture packets |
| Level    | Packet level    |
| Layer    | L2–L7           |
| Output   | Raw packets     |
| Skill    | Advanced        |

Syntax

```bash
tcpdump -i eth0
tcpdump -i eth0 port 80
tcpdump -i eth0 -w capture.pcap
```

Use Case

* Debug **real traffic**
* Security investigation
* API / microservice issues

---

🟣 `nmap`

| Item     | Details             |
| -------- | ------------------- |
| Function | Port & service scan |
| Protocol | TCP/UDP             |
| Layer    | L4–L7               |
| Type     | Active scanning     |
| Risk     | Detectable scan     |

Syntax

```bash
nmap 192.168.1.1
nmap -p 80,443 example.com
nmap -sS 192.168.1.0/24
```

Use Case

* Security audits
* Find open ports
* Infra validation

---

⚖️ Tool Comparison (Quick)

| Scenario            | Best Tool    |
| ------------------- | ------------ |
| Server reachable?   | `ping`       |
| Network delay?      | `traceroute` |
| App listening port? | `netstat`    |
| Packet-level debug? | `tcpdump`    |
| Security scan?      | `nmap`       |

---

## 8 Linux Networking (ip, ifconfig, route)

🔍 Command Overview Table

| Command      | Purpose                   | Replacement Status | Used In                |
| ------------ | ------------------------- | ------------------ | ---------------------- |
| **ip**       | Modern network management | ✅ Recommended      | All modern Linux       |
| **ifconfig** | Interface configuration   | ❌ Deprecated       | Old systems            |
| **route**    | Routing table view        | ❌ Deprecated       | Replaced by `ip route` |

---

🟢 `ip` Command (MOST IMPORTANT)

🔹 What it does

* Manage **IP address**
* Manage **network interfaces**
* Manage **routing table**

---

📘 `ip` Command – Detailed Table

| Task                    | Command                                | Explanation           |
| ----------------------- | -------------------------------------- | --------------------- |
| Show all interfaces     | `ip a`                                 | List interfaces + IPs |
| Show only UP interfaces | `ip link show up`                      | Active interfaces     |
| Bring interface up      | `ip link set eth0 up`                  | Enable interface      |
| Bring interface down    | `ip link set eth0 down`                | Disable interface     |
| Assign IP               | `ip addr add 192.168.1.10/24 dev eth0` | Set IP                |
| Remove IP               | `ip addr del 192.168.1.10/24 dev eth0` | Remove IP             |
| Show routing table      | `ip route`                             | Display routes        |
| Add default route       | `ip route add default via 192.168.1.1` | Set gateway           |
| Delete route            | `ip route del 10.0.0.0/24`             | Remove route          |

---

🟡 `ifconfig` Command (OLD but Asked in Interviews)

🔹 What it does

* View network interfaces
* Assign IP (legacy)

---

📘 `ifconfig` Command – Detailed Table

| Task                    | Command                                            | Explanation       |
| ----------------------- | -------------------------------------------------- | ----------------- |
| Show interfaces         | `ifconfig`                                         | All interfaces    |
| Enable interface        | `ifconfig eth0 up`                                 | Bring up          |
| Disable interface       | `ifconfig eth0 down`                               | Bring down        |
| Assign IP               | `ifconfig eth0 192.168.1.10 netmask 255.255.255.0` | Set IP            |
| Show specific interface | `ifconfig eth0`                                    | Interface details |

⚠️ **Note**: Not installed by default on modern Linux.

---

🔵 `route` Command (Legacy Routing)

🔹 What it does

* View & modify routing table

---

📘 `route` Command – Detailed Table

| Task                | Command                                     | Explanation    |
| ------------------- | ------------------------------------------- | -------------- |
| Show routes         | `route -n`                                  | Routing table  |
| Add default gateway | `route add default gw 192.168.1.1`          | Set gateway    |
| Delete route        | `route del default`                         | Remove gateway |
| Add network route   | `route add -net 10.0.0.0/24 gw 192.168.1.1` | Add route      |

---

🔄 Old vs New Command Mapping (IMPORTANT)

| Old Command        | New Command           |
| ------------------ | --------------------- |
| `ifconfig`         | `ip a`                |
| `ifconfig eth0 up` | `ip link set eth0 up` |
| `route -n`         | `ip route`            |
| `route add`        | `ip route add`        |

---

🧠 DevOps Real Use Cases

| Scenario             | Command             |
| -------------------- | ------------------- |
| Check server IP      | `ip a`              |
| Check gateway        | `ip route`          |
| Debug network issue  | `ip a` + `ip route` |
| Cloud VM networking  | `ip`                |
| Container networking | `ip`                |

---

## 9 Cloud Networking (VPCs, subnets, gateways)

☁️ AWS VPC Components – Full Explanation Table

| VPC Section                       | What it is            | Purpose / Use                    | DevOps / Real Use             |
| --------------------------------- | --------------------- | -------------------------------- | ----------------------------- |
| **Your VPCs**                     | Virtual Private Cloud | Private network in AWS           | Create isolated cloud network |
| **Subnets**                       | Network inside VPC    | Divide VPC into smaller networks | Public / Private subnets      |
| **Route Tables**                  | Routing rules         | Control traffic flow             | Internet / NAT routing        |
| **Internet Gateways (IGW)**       | Internet connector    | Allow public internet access     | Public EC2 access             |
| **Egress-only Internet Gateways** | IPv6 outbound gateway | IPv6 outbound only               | Secure IPv6 traffic           |
| **Carrier Gateways**              | Telecom routing       | Used with AWS Wavelength         | 5G / telecom apps             |
| **DHCP Option Sets**              | Network configs       | DNS, domain name                 | Custom DNS setup              |
| **Elastic IPs (EIP)**             | Static public IP      | Fixed public IP                  | Load balancers, NAT           |
| **Managed Prefix Lists**          | IP group list         | Reusable CIDR ranges             | Security rules simplification |
| **NAT Gateways**                  | Outbound internet     | Private subnet internet          | Secure updates                |
| **Peering Connections**           | VPC-to-VPC link       | Private VPC communication        | Multi-VPC architecture        |
| **Route Servers**                 | Dynamic routing       | Central route management         | Advanced networking           |

---

🔍 Important Ones (Must Know for DevOps)

1️⃣ Your VPCs

* CIDR block (example: `10.0.0.0/16`)
* Region-specific
* Fully isolated network

---

2️⃣ Subnets

| Type    | Internet | Example     |
| ------- | -------- | ----------- |
| Public  | Yes      | Web servers |
| Private | No       | Databases   |

---

3️⃣ Route Tables

Controls **where traffic goes**.

| Destination | Target           |
| ----------- | ---------------- |
| `0.0.0.0/0` | Internet Gateway |
| `0.0.0.0/0` | NAT Gateway      |

---

4️⃣ Internet Gateway

* Required for **public subnet**
* One IGW per VPC
* No IGW = no internet

---

5️⃣ NAT Gateway

* Allows **private subnet → internet**
* Blocks **internet → private subnet**
* Placed in **public subnet**

---

6️⃣ Elastic IP

* Static public IPv4
* Used with:

  * NAT Gateway
  * EC2
  * Load Balancer

---

7️⃣ VPC Peering

* Private connection
* No internet
* One-to-one connection

```
VPC-A ⇄ VPC-B
```

---

8️⃣ DHCP Option Sets

Controls:

* DNS server
* Domain name

Example:

```
AmazonProvidedDNS
```

---

🧠 VPC Traffic Flow (Simple)

```
User
 ↓
Internet
 ↓
Internet Gateway
 ↓
Public Subnet (EC2 / LB)
 ↓
Private Subnet (DB)
```
