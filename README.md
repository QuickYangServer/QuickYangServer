# QuickYangServer
Highly Scalable Netconf Yang server
In a YANG-based solution, the client and server are driven by the content of YANG modules. The server includes the definitions of the modules as meta-data that is available to the NETCONF engine. This engine processes incoming requests, uses the meta-data to parse and verify the request, performs the requested operation, and returns the results to the client.

                     +----------------------------+ 
                     |Server (device)             | 
                     |    +--------------------+  | 
                      |    |      configuration |  | 
           +----+     |    |     ---------------|  | 
           |YANG|+    |    | m d  state data    |  | 
           |mods||+   |    | e a ---------------|  | 
           +----+|| -----> | t t  notifications |  | 
            +----+|   |    | a a ---------------|  | 
             +----+   |    |      operations    |  | 
                      |    +--------------------+  | 
                      |           ^                | 
                      |           |                | 
                      |           v                | 
    +------+          |     +-------------+        | 
    |      | -------------> |             |        | 
    |Client| <rpc>    |     |  NETCONF    |        | 
    | (app)|          |     |   engine    |        | 
    |      | <------------  |             |        |   
    +------+ <rpc-reply>    +-------------+        |   
                    |       /        \           |   
                    |      /          \          |   
                    |     /            \         | 
                    | +--------+   +---------+   | 
                    | | config |   |system   |+  | 
                    | |  data- |   |software ||+ | 
                    | |   base |   |component||| | 
                    | +--------+   +---------+|| | 
                    |               +---------+| | 
                    |                +---------+ | 
                    +----------------------------+  
	    
To use YANG, YANG modules must be defined to model the specific problem domain. These modules are then loaded, compiled, or coded into the server.

The sequence of events for the typical client/server interaction may be as follows:

A client application ([C]) opens a NETCONF session to the server (device) ([S])
[C] and [S] exchange <hello> messages containing the list of capabilities supported by each side, allowing [C] to learn the modules supported by [S]
[C] builds and sends an operation defined in the YANG module, encoded in XML, within NETCONF's <rpc> element
[S] receives and parses the <rpc> element
[S] verifies the contents of the request against the data model defined in the YANG module
[S] performs the requested operation, possibly changing the configuration datastore
[S] builds the response, containing the response, any requested data, and any errors
[S] sends the response, encoded in XML, within NETCONF's <rpcreply> element
[C] receives and parses the <rpcreply> element
[C] inspects the response and processes it as needed
Note that there is no requirement for the client or server to process the YANG modules in this way. The server may hard code the contents of the data model, rather than handle the content via a generic engine. Or the client may be targeted at the specific YANG model, rather than being driven generically. Such a client might be a simple shell script that stuffs arguments into an XML payload template and sends it to the server.
  
  ------Please write to quickyangserver@gmail.com for further information or queries----------------------
