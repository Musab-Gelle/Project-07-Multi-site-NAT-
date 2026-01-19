# Project-07-Multi-site-NAT-
This project demonstrates a **multi-site network** with a HQ office, a Branch office, and Internet access, using **NAT overload (PAT)** to allow internal PCs to access the Internet while preventing inbound Internet connections to private networks.
# Overview
This project demonstrates a **multi-site network** with a HQ office, a Branch office, and Internet access, using **NAT overload (PAT)** to allow internal PCs to access the Internet while preventing inbound Internet connections to private networks.

---

# Network Design
- **HQ Router**
  - g0/0 → LAN HR, IT, Finance VLANs (inside NAT)
  - g0/1 → WAN to Branch (inside NAT)
  - g0/2 → WAN to ISP (outside NAT)
- **Branch Router**
  - g0/0 → Branch LAN
  - g0/1 → WAN to HQ
- **ISP Router**
  - g0/0 → WAN to HQ
  - g0/1 → Internet PC

---

# IP Addressing
| Device | Interface | IP Address | Role |
|--------|-----------|------------|------|
| HR PC | N/A | 192.168.10.x | LAN |
| IT PC | N/A | 192.168.20.x | LAN |
| Finance PC | N/A | 192.168.30.x | LAN |
| Branch PC | N/A | 192.168.40.x | LAN |
| HQ Router | g0/2 | 203.0.113.2 | NAT Outside |
| ISP Router | g0/0 | 203.0.113.1 | Internet Link |
| Internet PC | N/A | 8.8.8.8 | Internet Host |

---

# Lab Goals
1. Configure NAT overload (PAT) on HQ Router.
2. Allow all internal PCs to reach the Internet.
3. Prevent unsolicited inbound traffic from the Internet to internal PCs.
4. Maintain Branch ↔ HQ connectivity.

---

# Verification
- Internal PCs → Internet PC: `ping 8.8.8.8` ✅
- Internet PC → Internal PCs: `ping 192.168.x.x` ❌ (blocked by ACL)
- NAT translations on HQ Router: `show ip nat translations` ✅
- Routing verified on all routers: `show ip route` ✅

---

# Skills Demonstrated
- Static routing (HQ ↔ Branch)  
- PAT / NAT configuration  
- Access control for inbound traffic  
- Multi-site network setup in Packet Tracer 
