# sdn-access-control
# SDN-Based Access Control System

**Name:** Nishanth T Chigilar
**SRN:** PES1UG24CS302

---

## 📌 Project Overview

This project implements an **SDN-based Access Control System** using **Mininet** and the **Ryu controller**.
The system allows only authorized hosts to communicate within the network by enforcing a **whitelist policy**.

The controller dynamically installs **OpenFlow rules** to either **allow or block traffic** based on the source IP address.

---

## 🎯 Objectives

* Implement SDN controller–switch interaction
* Design and install OpenFlow match-action rules
* Enforce access control using a whitelist
* Block unauthorized hosts
* Validate functionality using testing and flow inspection

---

## 🧠 Key Concept

The controller checks incoming packets and:

* ✅ Allows traffic if the source IP is in the whitelist
* ❌ Blocks traffic if the source IP is not authorized

This demonstrates centralized control and dynamic policy enforcement in SDN.

---

## 🏗️ Network Topology

* 1 Switch (s1)
* 3 Hosts:

  * h1 → 10.0.0.1 (Authorized)
  * h2 → 10.0.0.2 (Authorized)
  * h3 → 10.0.0.3 (Unauthorized)

---

## ⚙️ Technologies Used

* Python (Ryu Controller)
* Mininet (Network Simulation)
* Open vSwitch (OVS)
* OpenFlow Protocol

---

## 🚀 Setup & Execution

### 1. Start Controller

```bash
cd ~/sdn-access-control
source ryu38-env/bin/activate
./ryu38-env/bin/ryu-manager access_control.py
```

### 2. Start Mininet

```bash
sudo mn --custom topo.py --topo mytopo --controller=remote --switch ovsk,protocols=OpenFlow13
```

---

## 🧪 Testing & Validation

### ✅ Allowed Communication

```bash
h1 ping h2
```

Result: Successful communication

---

### ❌ Blocked Communication

```bash
h3 ping h2
```

Result: Packet loss (access denied)

---

### 🔍 Flow Table Verification

```bash
sh ovs-ofctl -O OpenFlow13 dump-flows s1
```

Example rule:

```
nw_src=10.0.0.3 actions=drop
```

---

### 📊 Performance Test

```bash
iperf h1 h2
```

---

## 🔁 Regression Testing

After adding h3 to the whitelist:

* Traffic from h3 is allowed
* Flow rules update dynamically

---

## 📸 Output Evidence

* Ping results (allowed vs blocked)
* Flow table entries
* iperf results

---

## ✅ Conclusion

The project successfully demonstrates:

* Centralized network control using SDN
* Dynamic flow rule installation
* Effective access control using whitelist policy

This highlights the flexibility and power of SDN in managing network security.

---

## 📚 References

* Ryu SDN Framework Documentation
* Mininet Documentation
* OpenFlow Specifications
