## Overview

The Tangle is an evolving technology.  In the beginning, the assumption was more honest than dishonest transactions.  The first security mechanism was Proof of Work (PoW).  

However, Tangle developers realized that if an attacker exploited the PoW and took control of the majority of hashing power, then they might control the direction of consensus.  Thus, an attacker could double spend and split the network.
 
Enter the “coordinator”, a safety mechanism.  Such safety mechanisms are common in blockchain and DLT systems.  For example, Satoshi’s Bitcoin had hard-coded checkpoints plus an alerts system for him to shut down the network if necessary.
 
Like training wheels, the Coordinator prevents double spends until the network gains enough hashing power to be intrinsically secure.  When the Tangle gains critical mass, the coordinator will no longer be required.
 
Initially there was one Coordinator run by IOTA Foundation.  It issued a normal signed transaction called a “milestone”.  Consensus was achieved by a transaction being confirmed, if and only if, it was referenced by a milestone.  

### Replacing the Coordinator

Considerable research is underway towards a secure replacement for the Coordinator.  The first step, is releasing Compass, an open source coordinator.  Compass allows public nodes to generate milestones.  If an invalid milestone is released, then peer nodes will reject it.  Nodes can be ranked based on their reputation for releasing valid milestones.  

### Node Reputation
 
Nodes can be ranked by adapting a page ranking algorithm.  This type of ranking has been applied to Gnutella file-sharing network allowing users to make informed judgments of authenticity before downloading content.  The goal is to avoid the PoW race while making it impossible to double spend, as well as, penalizing spammers.

Nodes that achieve a high level of trustworthiness are called "Stars".  Stars issue reference transactions much like the IOTA Coordinator milestones, but the constellation of Stars is decentralized.

### Tip Selection
 
Research is also underway into the best tip selection.

### Private Tangle

Compass makes it possible to create a private Tangle.


 

