https://www.youtube.com/watch?v=rmFX1V49K8U&list=PLW8bTPfXNGdAZIKv-y9v_XLXtEqrPtntm

# General
- `Time To Live`
  Each time a system sends an IP packet, it initilized a field called TTL. usually between 64 128 or 255.
  Each time the packet hops over the network, this value is decremented. when it reaches zero, the packet is discarded.
  This can be used to estimate the number of hops, or routers the packet went through on its journey.
- 
- 

# Three Way Handshake
- Viewed in Wireshark as [SYN] Followed by [SYN, ACK] Followed by [ACK]

Sequence:
1. Client sends [Sync]
- `Source Port: 54846` is a temporary port used by the client (ephermal)
- Stream index: this is a wireshark thing, describes the 'conversation number' that enumerates all the tuples of the form [src_ip, dst_ip, port, port]
- `Sequence Number (raw): 1779687413`  - this is a BYTES counter that the clients sends to the server (ISN - initial sequence number) that tells the server how the clients enumerates its bytes. so that the server will know how to acknowledge properly on the number of bytes sent
  
2. Server sends [Syn, Ack]
   - `Acknowledgment number (raw): 1779687414` the server increments the raw sequence number by one so that the client knows the server is in sync about the enumeration of packets.
   - The server sends it own sequence number to the client so that the client could acknowledge correctly.
3. Client sends [ACK]
   - 
- Retransmissions
- Out Of Orders
- Window Problems
1. sdgfs
2. sdf
3. sdf
