## Overview

The Tangle is an evolving technology.  In the beginning, the assumption was more honest than dishonest transactions.  The first security mechanism was Proof of Work (PoW).  

However, Tangle developers realized that if an attacker exploited the PoW and took control of the majority of hashing power, then they might control the direction of consensus.  Thus, an attacker could double spend and split the network.
 
Enter the “coordinator”, a safety mechanism.  Such safety mechanisms are common in blockchain and DLT systems.  For example, Satoshi’s Bitcoin had hard-coded checkpoints plus an alerts system for him to shut down the network if necessary.
 
Like training wheels, the Coordinator prevents double spends until the network gains enough hashing power to be intrinsically secure.  When the Tangle gains critical mass, the coordinator will no longer be required.
 
Initially there was one coordinator run by IOTA Foundation.  It issued a normal signed transaction called a “milestone”.  Consensus was achieved by a transaction being confirmed, if and only if, it was referenced by a milestone.  

Now, an open source coordinator, called Compass, has been released.  Compass moves the Tangle towards true peer-to-peer consensus.  If an invalid milestone is issued, the rest of the nodes will reject it.
