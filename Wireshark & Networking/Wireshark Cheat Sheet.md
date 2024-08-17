
Preferences:
- disable prompting of unsaved work:
   _Edit -> Preferences -> Appearance -> Confirm unsaved capture files_.

Filters:
- output packets to telemetry QA:
```
ip.dst == 18.153.62.104 && tcp.dstport == 50051
```
- all traffic between 2 IP addresses
```
((ip.src == 192.168.3.3) &&(ip.dst == 192.168.3.13)) || ((ip.src == 192.168.3.13) &&(ip.dst == 192.168.3.3))
```
- only crane state msg:
```
((ip.src == 192.168.3.3) &&(ip.dst == 192.168.3.13)) || ((ip.src == 192.168.3.13) &&(ip.dst == 192.168.3.3)) && (_ws.col.info == "DATA[3] (GRPC) (PROTOBUF) ultraproto.CraneStateMsg")
```
- 