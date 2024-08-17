# Task 1: Network Segmentation
maybe we should segment the network so that all local devices use the same VLAN (virtual local area network)
   
   you can segment your network using VLANs (Virtual Local Area Networks) to separate the two devices onto different network segments. In this case, the devices would still have the same IP address, but they wouldn't be able to see each other due to being on different VLANs. You can then route traffic to the appropriate device based on the VLAN it's on.
   
To achieve your goal of having the cameras on each machine use the same IP addresses while preventing the machines from accessing each other's cameras, you can use network segmentation with VLANs. Here's a detailed approach:

### 1. **Setup VLANs (Virtual Local Area Networks):**
   - **VLAN 1 for Machine 1 and its Cameras**:
     - Assign a VLAN (e.g., VLAN 10) to Machine 1 and its connected cameras.
     - Assign the cameras connected to Machine 1 with static IP addresses (e.g., 192.168.1.x).
   - **VLAN 2 for Machine 2 and its Cameras**:
     - Assign a separate VLAN (e.g., VLAN 20) to Machine 2 and its connected cameras.
     - Assign the cameras connected to Machine 2 with the same static IP addresses as those used for the cameras in VLAN 1 (e.g., 192.168.1.x). These IPs are the same as in VLAN 10 but isolated due to being in a different VLAN.
   - **VLAN for Machine-to-Machine Communication**:
     - Assign a third VLAN (e.g., VLAN 30) dedicated to communication between the two machines. Assign unique IP addresses to the machines in this VLAN for direct communication.

### 2. **Configure Network Equipment:**
   - **Managed Switch Configuration**:
     - You’ll need a managed switch that supports VLANs. Configure ports connected to Machine 1 and its cameras to be in VLAN 10, and ports connected to Machine 2 and its cameras in VLAN 20.
     - Configure the port that connects the Wi-Fi device to allow VLAN 30 traffic for machine-to-machine communication.
   - **Wi-Fi Device Configuration**:
     - Ensure the Wi-Fi device is configured to handle traffic for VLAN 30, allowing the two machines to communicate without any VLAN conflicts.

### 3. **Routing and Access Control**:
   - **Routing Between VLANs**:
     - By default, VLANs are isolated from each other. To allow the machines to communicate while preventing access to the other machine’s cameras, ensure the routing is set up only between the machines' VLAN (VLAN 30). Do not route traffic between VLAN 10 and VLAN 20.
   - **Firewall Rules**:
     - You can use firewall rules to enforce that each machine can only access its VLAN’s cameras and the other machine via the VLAN 30 network. Block any traffic that attempts to cross from VLAN 10 to VLAN 20 and vice versa.

### 4. **Testing and Verification:**
   - **Test Communication**:
     - Ensure that each machine can communicate with its cameras and the other machine but cannot access the other machine’s cameras.
   - **Monitor Network**:
     - Use network monitoring tools to ensure that traffic flows as expected and there’s no cross-VLAN communication between the cameras of different machines.

### Benefits of This Setup:
- **Isolation:** Cameras with the same IP addresses on different VLANs will not conflict with each other since VLANs segment the network traffic.
- **Security:** The isolation prevents machines from accessing the other machine's cameras, ensuring privacy and security.
- **Flexibility:** This setup allows you to maintain the same IP addressing scheme for cameras across different machines, simplifying network management.

### Example:
- **Machine 1 and its cameras (VLAN 10):**
  - Machine 1 IP: 192.168.10.1 (in VLAN 10)
  - Camera IPs: 192.168.1.10, 192.168.1.11, etc. (in VLAN 10)
- **Machine 2 and its cameras (VLAN 20):**
  - Machine 2 IP: 192.168.20.1 (in VLAN 20)
  - Camera IPs: 192.168.1.10, 192.168.1.11, etc. (in VLAN 20, same as VLAN 10)
- **Machine-to-Machine communication (VLAN 30):**
  - Machine 1 VLAN 30 IP: 192.168.30.1
  - Machine 2 VLAN 30 IP: 192.168.30.2

This solution should give you the desired network setup with the benefits of VLAN-based segmentation and the ability to reuse IP addresses across isolated segments.


# Task 2: Network Capture on Gateworks SBC
   
To analyze the packets going through the radio using Wireshark, you have several options depending on your setup:

https://www.youtube.com/watch?v=DAtyzE1TUlI
### 1. **Install Wireshark on the SBC:**

- **Advantages:** Installing Wireshark directly on the SBC allows you to capture packets as they traverse the network bridge between the radio and the machine. This method is straightforward if the SBC has sufficient resources (CPU, memory, storage) to run Wireshark.
- **Disadvantages:** SBCs often have limited resources, so running Wireshark directly on the SBC might not be feasible, especially if the network traffic is heavy or if you need to capture for extended periods.

### 2. **Remote Packet Capture:**

- **Option 1: SSH and Dumpcap/Tcpdump on SBC:**
    - You can install a lightweight packet capture tool like `tcpdump` or `dumpcap` on the SBC and then use SSH to capture the packets remotely. The captured packets can either be saved to a file and transferred to another machine for analysis with Wireshark or streamed directly to Wireshark on your local machine using SSH.
- **Option 2: Wireshark’s Remote Capture Feature:**
    - Wireshark supports remote capture interfaces through tools like `rpcapd`. If the SBC supports `rpcapd`, you can capture packets on the SBC remotely from another machine running Wireshark.

### 3. **Port Mirroring on a Network Switch:**

- If your network includes a managed switch between the SBCs and the machines, you could configure port mirroring (also known as SPAN). This would mirror all traffic between the SBCs and the machines to another port where you can connect a machine running Wireshark.

### 4. **Inline Network Tap:**

- An inline network tap can be placed between the SBC and the radio or machine. This hardware device duplicates the traffic for monitoring purposes without interfering with the communication. The mirrored traffic can then be captured by a machine running Wireshark.

### 5. **Capture on the Machines Themselves:**

- If installing Wireshark on the SBC is not possible, you can capture traffic on the machines themselves. However, this approach will only show traffic that has already been processed by the machine and may miss some low-level radio communications.

### Summary:

- **Installing Wireshark on the SBC** is the simplest solution but may be resource-intensive.
- **Remote packet capture** provides flexibility, especially if the SBC has limited resources.
- **Port mirroring or network tap** offers a non-intrusive way to capture traffic but requires additional hardware or network configuration.

# Task 3: SW - Switch to BiDirectional communication
(either grpc or simple udb)

grpc uses TCP which might clutter the network in case of retransmissions etc

https://stackoverflow.com/questions/4810026/sending-protobuf-messages-with-boostasio

# Task 4:
https://www.gridconnect.com/blogs/news/900-mhz-the-wireless-workhorse


