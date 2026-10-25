# Virtual Network Simulation Lab

A small routed network built in **Cisco Packet Tracer** to practise establishing, monitoring and troubleshooting network systems (Yuva virtual internship task).

## What is in this repository

| Folder | Contents |
|---|---|
| `report/` | Full project report (Word and PDF) |
| `configs/` | Router CLI configuration scripts and end-device addressing |
| `screenshots/` | Evidence: topology, routing tables, ping/traceroute, Syslog, SNMP, Simulation mode, troubleshooting |
| `packet-tracer/` | The `.pkt` simulation file (add it here) |

## Topology

Two LANs joined by two routers over a /30 link.

| Network | Subnet |
|---|---|
| LAN1 (PC1, PC2, Server0) | 192.168.1.0/24 |
| LAN2 (PC3, PC4) | 192.168.2.0/24 |
| Router link | 10.0.0.0/30 |

Routing: RIP version 2 on both routers.

## Monitoring implemented

- **ping / tracert** between LANs (TTL 126, three-hop path)
- **Syslog** from both routers to Server0 (192.168.1.100)
- **SNMPv2c** queries from PC1 using the MIB Browser (sysDescr, sysName)
- **Simulation mode** packet capture (ICMP)

## Troubleshooting scenarios

1. **Router interface shut down** - ping failed with "Destination host unreachable" from the gateway; fixed with `no shutdown`.
2. **Wrong default gateway on PC3** - local ping worked, remote ping timed out; gateway corrected to 192.168.2.1.
3. **RIP process removed from Router2** - routes to the other LAN disappeared; RIP configuration re-applied.

## How to reproduce

1. Build the topology shown in `screenshots/01_topology_packet_tracer.png`.
2. Paste `configs/R1.txt` and `configs/R2.txt` into the router CLIs.
3. Set the end-device addresses from `configs/end_devices.txt` and switch the SYSLOG service on in Server0.
4. Verify with `ping`, `tracert`, `show ip route` and the SNMP MIB Browser.

See `report/Network_Simulation_Report.pdf` for the full explanation.
