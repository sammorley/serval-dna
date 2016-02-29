Route REST API
==============
[Serval Project][], March 2016

Introduction
------------

Every [Serval DNA][] daemon running on a node in the [Serval mesh network][]
maintains its own dynamic *routing table*, which it uses to choose the [network
interface][] on which to send each outgoing [MDP message][].  It updates its
routing table every time it receives an [overlay packet][].  For more details,
see [Mesh Datagram Protocol][].

The [Serval DNA][] daemon gives applications access to its routing table via
the **Route REST API** described in this document.  Applications can use this
information to:

  * discover the current [network peers](#peer)s
  * discover the currently reachable [nodes](#node)
  * discover whether any given [SID][] has recently been encountered
  * estimate the quality of service to any given reachable [node](#node)
  * work out the current topology of the nearby mesh network

Basic concepts
--------------

### Mesh routing

Whenever a [Serval DNA][] daemon running on a node in the [Serval mesh
network][] receives an [overlay packet][], it deduces the following facts:

  * at the time the packet was received, there was a [direct link](#link) with
    the [transmitting node](#transmitter), so the transmitter's [SID][] and all
    of its [zero-hop](#zero-hop) SIDs can be marked as [network peers](#peer)

  * the [sender][] of every [MDP message][] within the packet was very
    recently [reachable](#reachable) via the transmitter

Every daemon regularly announces its presence by periodically [broadcast][]ing a [MDP
message][] on all of its [configured][] [network interface][]s.  Any broadcast message generated
by a local client application will serve, and if none are sent 

Each broadcast
message contains its own [primary SID](#primary-sid) as the sender address.

in order to detect the
[identities][] of all other daemons within range (on wireless interfaces) or on
the same network segment (on wired interfaces).

### Node

TBC

### Peer

TBC

### Primary SID

TBC

### Zero hop

TBC

### Reachable

TBC

REST Requests
-------------

### GET /restful/route/all.json

Returns a list of all currently known identities, in [JSON table][] format.
The table columns are:

*   **sid**: the [SID](#serval-id) of the identity, a string of 64 uppercase
    hex digits
*   **did**: the optional [DID][] (telephone number) of the identity, either
    *null* or a string of five or more digits from the set `123456789#0*`
*   **name**: the optional name of the identity, either *null* or a non-empty
    string of [UTF-8] characters

### GET /restful/route/reachable.json

### GET /restful/route/peers.json

-----
**Copyright 2015 Serval Project Inc.**  
![CC-BY-4.0](./cc-by-4.0.png)
Available under the [Creative Commons Attribution 4.0 International licence][CC BY 4.0].


[Serval Project]: http://www.servalproject.org/
[CC BY 4.0]: ../LICENSE-DOCUMENTATION.md
[Serval Mesh network]: http://developer.servalproject.org/dokuwiki/doku.php?id=content:tech:mesh_network
[Serval DNA]: ../README.md
[REST-API]: ./REST-API.md
[SID]: ./REST-API-Keyring.md#serval-id
[overlay packet]: ./Mesh-Datagram-Protocol.md#overlay-packet
[sender]: ./Mesh-Datagram-Protocol.md#sender
[transmitter]: ./Mesh-Datagram-Protocol.md#transmitter
[MDP message]: ./Mesh-Datagram-Protocol.md#mdp-message
[Mesh Datagram Protocol]: ./Mesh-Datagram-Protocol.md
[JSON table]: ./REST-API.md#json-table
[configured]: ./Servald-Configuration.md
[network interface]: ./Servald-Configuration.md#network-interfaces
[200]: ./REST-API.md#200-ok
[201]: ./REST-API.md#201-created
[202]: ./REST-API.md#202-accepted
[400]: ./REST-API.md#400-bad-request
[404]: ./REST-API.md#404-not-found
[419]: ./REST-API.md#419-authentication-timeout
[422]: ./REST-API.md#422-unprocessable-entity
[423]: ./REST-API.md#423-locked
[500]: ./REST-API.md#500-server-error
