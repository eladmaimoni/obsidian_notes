1. When opening the SW on TC2 - seems to receive packets from TC1
   - note: trolley camera seemed to be out of battery
   - occasional communication loss at SW level
1. we trasferred both cranes to joystick mode (since ABB was at maintanence) in order to have relatively constant packet send frequency - 50ms 
   - we examined constant packet transmission freq on TC2
   - recv on TC2 had occasional disconnections
2. We cancelled TC1 packet receive so that we will only have communication TC1 -> TC2
   - we still witnessed occasional communication loss - MAYBE less frequent
   - SW profiling was OK - no problem there
   - wireshark - TC2 only sends TCP ACK as expected (nothing else)
   - wireshark - TC2 ack had occasional retransimssions of ACK
   - SW - TC2 packet
   - scanning
    ![[Pasted image 20240816160947.png]]
Ideas:
- maybe analyze wireshark on SBC?
  To analyze the packets going through the radio using Wireshark, you have several options depending on your setup:

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

Choose the method that best fits your resources and network architecture.
- maybe we should reduce the packet size? simple protocol?
- try grpc compression?
```
#include <grpcpp/grpcpp.h> #include <grpcpp/support/client_context.h> grpc::ClientContext context; context.set_compression_algorithm(GRPC_COMPRESS_GZIP); // or GRPC_COMPRESS_DEFLATE
```
- maybe we should sync the message sending (ping-pong)
- what will happen when there are more than 2 nodes?
- how to decide who is the client and who is the server?
  - SIMPLE - the LOWER crane id is the SERVER, the higher is the CLIENT
Anti Collision:
- trolley out works - trolley in does not

