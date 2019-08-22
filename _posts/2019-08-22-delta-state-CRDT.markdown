---
layout: post
title:  "Reading note -- Delta state replicated data types"
date:   2019-08-22 10:12:19 +0200
categories: reading list
---
[Paper source here](https://arxiv.org/abs/1603.01529)
- Journal: Journal of Parallel and Distributed Computing，Volume 111, January 2018, Pages 162-173
- Author: [Paulo Sérgio Almeida](), [Ali Shoker]()，[CarlosBaquero]()

### Highlights:
> - Definition of delta-state CRDTs and their relation to state CRDTs.
> - Proofs of conditions to attain equivalence to state based CRDTs.
> - Anti-entropy algorithm for basic and causally consistent convergence.
> - Portfolio of delta state CRDTs including optimized sets, and recursive map.

### Motivation:
- Conflict-free replicated data types (CRDTs) are widely used for achieving eventual consistency for many systems.
- State-based CRDTs (CvRDTs) requires to send the entire state for communication, causing communication overhead.
- Operation-based CRDTs (CmRDTs) reduces message size but requires the communication layer to support **reliable exactly-once causal broadcast**.

### Solution:
> rethink the way state-based CRDTs should be designed, having in mind the problematic shipping of the entire state. Our aim is to ship a representation of the effect of recent update operations on the state, rather than the whole state, while preserving the idempotent nature of join.

#### System model:
State-based CRDTs:

![s-crdt](http://www.sciweavers.org/upload/Tex2Img_1566479562/render.png)

![s-crdt](http://www.sciweavers.org/upload/Tex2Img_1566479633/render.png)

Delta-based CRDTs:

![d-crdt](http://www.sciweavers.org/upload/Tex2Img_1566479694/render.png)

![d-crdt](http://www.sciweavers.org/upload/Tex2Img_1566479801/render.png)

It will be useful to find a non-trival decomposition such that delta-states returned by delta-mutators are smaller than the resulting state:

![d-crdt](http://www.sciweavers.org/upload/Tex2Img_1566479957/render.png)
#### Properties:
- State convergence
- Causual consistency

#### Examples:
- delta-GCounter
![delta-GCounter](/loc_pictures/delta_GCounter.png)

- delta-GSet
![delta-GSet](/loc_pictures/delta_GSet.png)

- delta-2PSet
![delta-2PSet](/loc_pictures/delta_2Pset.png)

- delta-LWWSet
![delta-LWWSet](/loc_pictures/delta_LWWSet.png)
### Related works:
- Eventually convergent data types
- Message size
- Encoding causal histories
