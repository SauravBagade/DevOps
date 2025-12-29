# Networking – Commands (Complete Reference)

## A) DNS Commands

| Command            | Purpose             | Example                |
| ------------------ | ------------------- | ---------------------- |
| `nslookup`         | Basic DNS lookup    | `nslookup google.com`  |
| `dig`              | Detailed DNS query  | `dig google.com`       |
| `host`             | Simple DNS resolver | `host google.com`      |
| `resolvectl`       | System DNS status   | `resolvectl status`    |
| `/etc/resolv.conf` | DNS config file     | `cat /etc/resolv.conf` |

---

## B) Routing & Path Commands

| Command        | Purpose              | Example                |
| -------------- | -------------------- | ---------------------- |
| `ip route get` | Route to destination | `ip route get 8.8.8.8` |
| `tracepath`    | Path + MTU discovery | `tracepath google.com` |
| `mtr`          | Ping + traceroute    | `mtr google.com`       |
| `arp`          | View ARP table       | `arp -a`               |
| `ip neigh`     | ARP cache (modern)   | `ip neigh show`        |

---

## C) Port & Socket Commands

| Command   | Purpose         | Example          |
| --------- | --------------- | ---------------- |
| `ss`      | Modern netstat  | `ss -tulnp`      |
| `lsof -i` | Ports in use    | `lsof -i :80`    |
| `fuser`   | Port to process | `fuser 8080/tcp` |

---

## D) Firewall Commands (Linux)

| Command            | Purpose            | Example                   |
| ------------------ | ------------------ | ------------------------- |
| `iptables`         | Low-level firewall | `iptables -L`             |
| `iptables-save`    | Export rules       | `iptables-save`           |
| `iptables-restore` | Import rules       | `iptables-restore`        |
| `ufw`              | Simple firewall    | `ufw status`              |
| `firewall-cmd`     | RHEL firewall      | `firewall-cmd --list-all` |

---

## E) Network Interface Utilities

| Command   | Purpose            | Example            |
| --------- | ------------------ | ------------------ |
| `nmcli`   | NetworkManager CLI | `nmcli dev status` |
| `nmtui`   | Network UI         | `nmtui`            |
| `ethtool` | NIC details        | `ethtool eth0`     |
| `iw`      | Wireless info      | `iw dev`           |

---

## F) Connectivity & Transfer Tools

| Command       | Purpose          | Example              |
| ------------- | ---------------- | -------------------- |
| `curl`        | HTTP/API testing | `curl -I google.com` |
| `wget`        | File download    | `wget file.zip`      |
| `telnet`      | Port testing     | `telnet host 80`     |
| `nc` (netcat) | Network debug    | `nc -zv host 443`    |

---

## F.1) Sending Traffic / Data Commands (NEW)

| Command              | Purpose               | Example                                                         |
| -------------------- | --------------------- | --------------------------------------------------------------- |
| `curl -X GET`        | Send HTTP GET request | `curl -X GET https://api.example.com`                           |
| `curl -X POST`       | Send HTTP POST data   | `curl -X POST -d "name=test" https://api.example.com`           |
| `curl -H`            | Send custom headers   | `curl -H "Authorization: Bearer token" https://api.example.com` |
| `curl --data-binary` | Send raw payload      | `curl --data-binary @file.json https://api.example.com`         |
| `nc` send data       | Send TCP data         | `echo "hello" \| nc host 9000`                                  |
| `nc -u`              | Send UDP packet       | `echo "ping" \| nc -u host 514`                                 |
| `telnet` send        | Manual request        | `telnet host 80` then type HTTP                                 |
| `iperf3 -c`          | Send traffic load     | `iperf3 -c server_ip`                                           |
| `ab`                 | Send HTTP load        | `ab -n 1000 -c 10 http://site/`                                 |
| `hey`                | HTTP load testing     | `hey -n 1000 http://site/`                                      |

------|--------|--------|
| `curl` | HTTP/API testing | `curl -I google.com` |
| `wget` | File download | `wget file.zip` |
| `telnet` | Port testing | `telnet host 80` |
| `nc` (netcat) | Network debug | `nc -zv host 443` |

---

## G) Cloud Networking (AWS CLI)

| Command                            | Purpose        |
| ---------------------------------- | -------------- |
| `aws ec2 describe-vpcs`            | List VPCs      |
| `aws ec2 describe-subnets`         | List subnets   |
| `aws ec2 describe-route-tables`    | Routing tables |
| `aws ec2 describe-security-groups` | Firewall rules |
| `aws ec2 describe-nat-gateways`    | NAT gateways   |

---

## H) Kubernetes Networking Commands

| Command                    | Purpose         | Example                        |
| -------------------------- | --------------- | ------------------------------ |
| `kubectl get svc`          | Services        | `kubectl get svc`              |
| `kubectl get endpoints`    | Service IPs     | `kubectl get ep`               |
| `kubectl get pods -o wide` | Pod IPs         | `kubectl get pods -o wide`     |
| `kubectl describe svc`     | Service routing | `kubectl describe svc`         |
| `kubectl exec`             | Network testing | `kubectl exec -it pod -- curl` |

---

## I) Docker Networking Commands

| Command                  | Purpose         | Example                         |
| ------------------------ | --------------- | ------------------------------- |
| `docker network ls`      | List networks   | `docker network ls`             |
| `docker network inspect` | Network details | `docker network inspect bridge` |
| `docker inspect`         | Container IP    | `docker inspect container`      |

---

## J) System Network Information

| Command          | Purpose              |            |
| ---------------- | -------------------- | ---------- |
| `hostname -I`    | Show IP addresses    |            |
| `ip -s link`     | Interface statistics |            |
| `watch ip route` | Live routing view    |            |
| `dmesg           | grep eth`            | NIC errors |

---

## K) Packet Capture & Deep Debugging (MISSING)

| Command       | Purpose                  | Example                   |
| ------------- | ------------------------ | ------------------------- |
| `tcpdump`     | Packet capture           | `tcpdump -i eth0`         |
| `tcpdump -nn` | Disable DNS/port resolve | `tcpdump -nn port 80`     |
| `tcpdump -w`  | Save pcap file           | `tcpdump -w traffic.pcap` |
| `tshark`      | CLI Wireshark            | `tshark -i eth0`          |

---

## L) Bandwidth & Performance (MISSING)

| Command     | Purpose             | Example         |
| ----------- | ------------------- | --------------- |
| `iftop`     | Interface bandwidth | `iftop -i eth0` |
| `nload`     | Live bandwidth      | `nload eth0`    |
| `bmon`      | Bandwidth monitor   | `bmon`          |
| `iperf3 -s` | Start server        | `iperf3 -s`     |

---

## M) Advanced Socket & Kernel Networking (MISSING)

| Command           | Purpose         | Example                      |
| ----------------- | --------------- | ---------------------------- |
| `ss -s`           | Socket summary  | `ss -s`                      |
| `sysctl net.ipv4` | Kernel tuning   | `sysctl net.ipv4.ip_forward` |
| `sysctl -a`       | View all params | `sysctl -a`                  |

---

## N) Linux Network Namespace (CRITICAL FOR K8s / Docker)

| Command         | Purpose            | Example                         |
| --------------- | ------------------ | ------------------------------- |
| `ip netns list` | List namespaces    | `ip netns list`                 |
| `ip netns exec` | Run inside NS      | `ip netns exec ns ping 8.8.8.8` |
| `lsns -t net`   | Network namespaces | `lsns -t net`                   |

---

## O) Bridge & Virtual Networking (MISSING)

| Command       | Purpose        | Example            |
| ------------- | -------------- | ------------------ |
| `brctl show`  | Bridge info    | `brctl show`       |
| `bridge link` | Bridge ports   | `bridge link`      |
| `bridge vlan` | VLAN on bridge | `bridge vlan show` |

---

## P) VLAN & Traffic Control (ADVANCED – REAL DEVOPS)

| Command    | Purpose         | Example                |
| ---------- | --------------- | ---------------------- |
| `tc qdisc` | Traffic shaping | `tc qdisc show`        |
| `tc class` | Bandwidth class | `tc class show`        |
| `vconfig`  | VLAN config     | `vconfig add eth0 100` |

---

## Q) Proxy & Env Networking (OFTEN MISSED)

| Command             | Purpose      | Example                            |      |             |
| ------------------- | ------------ | ---------------------------------- | ---- | ----------- |
| `env                | grep proxy`  | Proxy vars                         | `env | grep proxy` |
| `export http_proxy` | Set proxy    | `export http_proxy=http://ip:port` |      |             |
| `no_proxy`          | Bypass proxy | `no_proxy=localhost,127.0.0.1`     |      |             |

---

## R) Cloud-Native Networking (MISSING)

| Command                                    | Purpose     |
| ------------------------------------------ | ----------- |
| `aws ec2 describe-network-interfaces`      | ENIs        |
| `aws ec2 describe-internet-gateways`       | IGWs        |
| `aws ec2 describe-vpc-peering-connections` | VPC Peering |
| `aws ec2 describe-vpn-connections`         | VPN         |

---

## S) Kubernetes CNI Debugging (ADVANCED)

| Command                     | Purpose        | Example                     |
| --------------------------- | -------------- | --------------------------- |
| `kubectl get nodes -o wide` | Node IPs       | `kubectl get nodes -o wide` |
| `kubectl get netpol`        | Network policy | `kubectl get netpol`        |
| `kubectl describe pod`      | Pod networking | `kubectl describe pod`      |
| `kubectl logs kube-proxy`   | Proxy issues   | `kubectl logs kube-proxy`   |

---

## T) Docker Advanced Networking (MISSING)

| Command                     | Purpose          | Example                             |
| --------------------------- | ---------------- | ----------------------------------- |
| `docker network create`     | Create network   | `docker network create net1`        |
| `docker network connect`    | Attach container | `docker network connect net1 c1`    |
| `docker network disconnect` | Detach           | `docker network disconnect net1 c1` |

---

## U) Systemd Networking (MODERN LINUX)

| Command            | Purpose        | Example                       |
| ------------------ | -------------- | ----------------------------- |
| `networkctl`       | Network status | `networkctl status`           |
| `resolvectl query` | DNS query      | `resolvectl query google.com` |

---

## DevOps Troubleshooting Flow (Recommended)

```
ping
→ traceroute / mtr
→ ip a / ip route
→ ss / lsof
→ tcpdump
→ firewall (iptables / SG)
→ curl / nc
```
---