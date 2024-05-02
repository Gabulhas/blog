---
title: "Writing a Distributed-Directory Database in Rust"
date: 2023-11-15T02:06:43+0000
draft: false
---

Btw, this is not finished yet, and read this more as a devlog.

As some sort of followup to my Bachelor's final project, I plan to implement something similar but with a real use case.

I will write this to force myself into actually making this.

The [project](https://github.com/Gabulhas/Arrow-Distributed-Directory-Protocol) was both a Node implementation and "Live" Visualization of the protocol.
Basically, it would start multiple nodes of this protocol/algorithm and then it boots a separate/independent node that receives information from the other ones and displays in a webpage the current state of the network.


# Arrow Distributed Directory Protocol
This is the [protocol](https://cs.brown.edu/people/mph/DemmerH98/disc.pdf) (ADDP) I implemented. There are a few similar, which could be variants/a definition of what I plan to do, but I will try to explain it briefly.

There are 3 main things in the network formed by this protocol:
- An object - Imagine it is like an actual data (or the ownership/exclusive access to it), like a file, a database entry, anything
- Links - Connections between Nodes. They are unidirectional, and when a request passes through it, the direction of the link gets reversed. So if a Link is pointing from A to B, and A forwards a request to B using the Link, the Link gets reversed and points from B to A instead.
- The Nodes - They either have the object, don't have it or they are requesting it. In other words, there are these types of nodes (that keep changing depending on their actions):
  - Owner - They own the object
  - Owner with Request - They own the object, but a request reached it, so they will have to send to the requester
  - Idle - They just forward requests they receive, they don't do anything else
  - Waiter - They made a request, they are waiting for the object (either the request is traveling through the network or the owner hasn't sent it the object)
  - Waiter with Request - Same as the Waiter, but other Waiter **B** in the network also requested the object and the Waiter **A** received it. So instead of forwarding it to the owner, the Waiter **A** holds on the request from **B** until itself receives the object, and only after it sends the object to the Waiter **B**.


Because of the mechanism of a link being reverted when a message passes through it, where it reverses, the connections always point to a node that is or will be a owner (in other words, that is or was a Waiter).

The fact that
- a node has to wait for an object to be sent
- when a request reaches the current owner, the link used to get to it gets reversed, all new requests will be forwarded to the source of the request
The object has an mutually exclusive access



# Distributed-Directory Database


What I'm trying to do is a distributed database that uses Arrow Distributed Directory Protocol in order to maintain an exclusive access to values.

Basically trying to find a problem to the solution 🤣.


But I want to implement everything "from scratch", from the Database aspect, to the Protocol aspect.

I want to build a "directory" per entry on the database.
When you read the original paper on ADDP you will see a "pre-configured" directory. The directory is already defined, and there's not even a mention or the concept of what happens when a node is added to the network, or how a directory is formed in the first place.

The directories must be a [Minimum Spanning Tree](https://en.wikipedia.org/wiki/Minimum_spanning_tree). I want this to be formed in a distributed way, independently per entry in the database (I'm assuming that an entry is an object).

So we need to also define a mechanism to form this MST in a decentralized way, and in a way that nodes won't always use the same neighbors.

Wouldn't make sense to broadcast a new entry to the whole network, as the purpose of having this kind of algorithm is to avoid such thing. Quoting the original paper "broadcast is impractical, so a directory structure must provide a way to navigate and synchronize by point-to-point communication."

Wouldn't make sense to always choose the same neighbors in case of a new object is added, as would also create "hotspots", as also, other purpose of these algorithms is to avoid such thing. Quoting the original paper "As
the number of nodes grows, or if an object is a \hot spot", that object's home is likely to become a synchronization bottleneck, since it must mediate all access to that object. ".

We want to have the same benefits of using these protocols/algorithms while "developing" the network, as more and more objects are added.

There are some variations, [Ivy](https://systems.cs.columbia.edu/ds2-class/papers/li-ivy.pdf) and [Arvy](https://github.com/infinisil/arvy/blob/master/thesis/Thesis.pdf). Would be interesting for the users of this software to also select which ones to use. They mostly differ on creation of the links.
- Arrow never changes the tree. When a request passes through a link, the link is only reversed. Connections are maitained, only the directions are reversed. Ex: If a request passes through the link A->B, the link s reversed to B->A
- Ivy changes the tree. When a request passes through a link, the link changes the destination to the source of the request. Ex: If a request passes through the link A->B and the source of the request was the node C, now that link is B->C.
- Arvy changes the tree also. Instead of a new link pointing to the origin of the request, it now points to a random node where the request passed through. Ex: The request passed the following path A->B->C->D->E, and now it's passing through the link E->F, the node F now can point to any of the nodes in the path (at random).
They always maintain a MST.

These protocols don't really mention partition tolerance or failures. If a node is down, the request should find another path. So the nodes should make a different type of request to known neighbors to hopefully find a different path.

Either that or, whenever we refer to a "node", we are actually referring to a cluster of machines (smaller nodes/inner nodes), and these clusters form a node in the directory.
To improve even more the network reliability, clusters shouldn't always be made of the same machines. An inner node can belong to a directory node (a cluster) when talking about a specific object directory, but for another different directory it should belong to a different cluster that form a directory node.
But having a whole cluster receiving a single request of a specific object, would increase the number of messages, so, when a cluster has a link to another cluster, it should select a random or a set of random nodes in the cluster.
We also need to find a mechanism to enforce that only one node or a set of nodes in the cluster takes care of a single request at a time (for a specific object).

So, summarized:
- I need a way to create new directories in a distributed manner.
- I need a way to force random selection of neighbors when creating new directories.
- I should provide ways for the user to select between Arrow, Ivy and Arvy.
- Requests should find different path (by requesting the neighbors) if a node is down.
- If a new KV is added, the node should check in the network (by recursively asking peers or maybe some other way) if a specific Key already exists. Either that or the K is always the hash of a V.
- When adding or removing a key, this info should be gossiped to create or destroy the directory
- We should have a different definition of nodes, as we may want to have actually a cluster of nodes to form a single "directory node"
- There should be clusters where:
  - In clusters, an inner node should actually belong to different clusters of nodes when referring to a directory of an object
  - Links should have info of a whole cluster, either
    - so it's possible to select a specific node or a set of nodes, so the whole cluster doesn't have to receive the
    - so other nodes in cluster function only has replicas and one is the master. When the master has a failure, another node should take it's place


# Implementation

In this section I will go through the implementation or commits as I develop this project. As of the writing of this phrase I don't even have a directory for the project in my machine.






