## Basic Concept
Exchange of data through the SUI network can be done between any Web2 or Web3 application that includes the DTP and Sui SDKs.

An application will first want to create its own "unique contact point" on the network by creating a "Host Sui Object" using the DTP API.

An application can "ping" or "connect" to other Host object created by other apps. Each Host are uniquely identified by a "Sui Object ID".

The typical `#!Rust <IP address>:<Port>` becomes a `#!Rust <Host Object ID>:<Port>`

## On-Chain Firewall

For security reason, each Host Object are by default created "completely closed". Using the DTP API, an application can choose to open ports of its Host object to progressively add services.

Other application will be able to observe what other Host allow/block even before attempting to use their service. Even if an attacker try to use a service when they should not, it will be rejected by the DTP Move package on-chain, therefore have no impact on the destination.

The DTP API allows fine grain control of allowance/blocking of particular requester, connection count or bandwidth limit. Configuration are kept and applied 24/7 on-chain.

## Connection Type and Escrow

DTP provides traditional byte streaming (TCP-Like) connections between Host, but also the simplification of higher level connection, in particular RPC calls.

When configuring a service for your Host, you must choose a "Service Level Agreement" that DTP will enforce.

An example is to require the requester to pay for the cost of the response that your server will have to provide.

!!! info "This is a good example where adding Web3 qualities to an existing Web2 service creates API monetization without requiring huge security/edge infrastructure investments"

DTP defines a set of "Typical" service level agreement to help minimize market confusion. 

| Service Level Agreement | Who Pays                                                 |
| ----------------------- | -------------------------------------------------------- |
| OpenDataStream          | Everyone pay for their own transactions (txns).          |
| AudioStream-Free        | Broadcaster only.                                        |
| JSON-RPC-BestEffort     | Everyone pay for their own txns. No response guaranteed. |
| JSON-RPC-RequesterPaid  | RPC Requester pays. Responder refunded through escrow.   |
| Ping-RequesterPaid      | RPC Requester pays. Responder refunded through escrow.   |

The requester agree to the SLA upon creation of the connection and is enforced through DTP escrow for the connection duration. DTP handles the fund redistribution fairly with consideration of various success/failure criteria (more refinement will follow in ~2024).
       
      
       