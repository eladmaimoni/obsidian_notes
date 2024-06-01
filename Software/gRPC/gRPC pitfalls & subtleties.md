1. Timeout on streaming RPCs
   - Soes not mean timeout for a single write / read within the stream
   - It means timeout for the whole stream
   - this may actually cause the stream to 'fail' after the timeout
   - hence - timeouts are not used for long lived streaming RPCs
2. Load Balancing contradicts long living streaming RPCs
   - load balancing - decide which backend will serve the call is made on a per RPC basis
3. dfhf
4. dfhfg
5. fgjgf