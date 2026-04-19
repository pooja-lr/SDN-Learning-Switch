# SDN Learning Switch Controller using POX

Member1:
Name: Pooja L R
 SRN: PES1UG24AM475

Member2:
Name: Edwin Himax
 SRN: PES1UG24AM430

Member3:
Name: Pratik Mallappa Kalloli 
 SRN: PES1UG24AM444

## 📌 Problem Statement

Implement an SDN controller that mimics a **learning switch** by dynamically learning MAC addresses and installing forwarding rules. The controller should handle incoming packets, learn source MAC addresses, and install flow rules to enable efficient packet forwarding.

---

## 🎯 Objective

* To understand SDN architecture and controller-switch interaction
* To implement MAC address learning logic
* To dynamically install flow rules in the switch
* To validate packet forwarding using Mininet

---

## 🛠️ Tools & Technologies Used

* **Mininet** – Network simulation
* **POX Controller** – SDN controller
* **Open vSwitch (OVS)** – Virtual switch
* **Python** – Controller logic implementation
* **WSL (Ubuntu)** – Execution environment

---

## ⚙️ Setup & Execution Steps

### 1. Install Required Packages

```bash
sudo apt update
sudo apt install git python3 python3-pip mininet openvswitch-switch -y
```

---

### 2. Clone POX Controller

```bash
cd ~
git clone https://github.com/noxrepo/pox.git
```

---

### 3. Create Learning Switch Controller

```bash
cd ~/pox/pox/misc
nano learning_switch.py
```

Paste the controller code and save the file.

---

### 4. Run POX Controller

```bash
cd ~/pox
python3 pox.py misc.learning_switch
```

---

### 5. Start Mininet Topology

(Open a new terminal)

```bash
sudo service openvswitch-switch start
sudo mn -c
sudo mn --topo single,3 --controller remote --switch ovsk
```

---

### 6. Test Connectivity

Inside Mininet:

```bash
pingall
h1 ping h2
```

---

### 7. View Flow Table

(Open another terminal while Mininet is running)

```bash
sudo ovs-ofctl dump-flows s1
```

---

### 8. Performance Testing (Optional)

```bash
iperf
```

---

## 📊 Expected Output

* All hosts successfully communicate (**0% packet loss**)
* Controller learns MAC addresses dynamically
* Flow rules are installed in the switch
* Reduced flooding after initial packet transmission

---

## 📸 Screenshots (Proof of Execution)

### Controller Running
![Controller](images/controller.png)

### Mininet Topology
![Topology](images/topology.png)

### Ping Test
![Pingall](images/pingall.png)

### Manual Ping
![Manual Ping](images/manual_ping.png)

### Flow Table
![Flow Table](images/flow_table.png)

---

## 🧠 Working Explanation

1. When a packet arrives at the switch, it is sent to the controller (`packet_in`)
2. The controller learns the **source MAC address and port mapping**
3. If the destination MAC is known:

   * A flow rule is installed
   * Packet is forwarded directly
4. If unknown:

   * Packet is flooded to all ports
5. Over time, the switch behaves like a **learning switch** with efficient forwarding

---

## ⚠️ Limitations

* iperf testing was partially limited due to WSL networking constraints, however latency and flow rule validation confirm correct functionality.
* Initial packets are flooded before learning occurs

---

## 📚 References

* POX Controller Documentation
* Mininet Documentation
* OpenFlow Switch Specification

---

## ✅ Conclusion

The project successfully demonstrates an SDN-based learning switch using POX. The controller dynamically learns MAC addresses, installs flow rules, and ensures efficient packet forwarding, fulfilling all project requirements.

---
