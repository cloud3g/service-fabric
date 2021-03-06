# Federation subsystem

The **Federation subsystem** uses the communication primitives provided by the [Transport subsystem](/src/prod/src/Transport#transport-subsystem) and stitches the various nodes into a single unified cluster that it can reason about. It provides the distributed systems primitives needed by the other subsystems - failure detection, [leader election](/src/prod/src/Federation/VoterStore.cpp), and [consistent routing](/src/prod/src/Federation/RoutingManager.cpp). The federation subsystem is built on top of distributed hash tables with a 128-bit token space. The subsystem creates a [ring topology over the nodes](/src/prod/src/Federation/NodeRing.cpp), with each node in the ring being allocated a subset of the token space for ownership. For failure detection, the layer uses a leasing mechanism based on heart beating and arbitration. The federation subsystem also guarantees through intricate [join](/src/prod/src/Federation/JoinManager.cpp) and departure protocols that only a single owner of a token exists at any time. This provides leader election and consistent routing guarantees. 
