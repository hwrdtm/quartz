---
title: "Conflict-free Replicated Data Types"
tags:
- learning/crdt
---

For plain text documents there are plenty of CRDT algorithms, such as [RGA](http://csl.snu.ac.kr/papers/jpdc11.pdf), [Causal Trees](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.994.4371&rep=rep1&type=pdf), [YATA](https://www.researchgate.net/publication/310212186_Near_Real-Time_Peer-to-Peer_Shared_Editing_on_Extensible_Data_Types), [WOOT](https://hal.inria.fr/file/index/docid/108523/filename/OsterCSCW06.pdf), [Treedoc](https://hal.inria.fr/inria-00445975/document), [Logoot](https://hal.inria.fr/inria-00432368/document), [LSEQ](https://hal.archives-ouvertes.fr/file/index/docid/921633/filename/fp025-nedelec.pdf), and various others.

CRDTs as primitives for local-first software.
- Special thing about them is that they are multi-user from the ground up.
- The only type of change that a CRDT cannot automatically resolve is when multiple users concurrently update the same property of the same object; in this case, the CRDT keeps track of the conflicting values, and leaves it to be resolved by the application or the user.
- CRDTs have some similarity to version control systems like Git, except that they operate on richer data types than text files.

### Resources

For a more technical introduction to CRDTs:
-   Alexei Baboulevitch’s [Data Laced with History](http://archagon.net/blog/2018/03/24/data-laced-with-history/)
-   Martin Kleppmann’s [Convergence vs Consensus](https://www.youtube.com/watch?v=B5NULPSiOGw) ([slides](https://speakerdeck.com/ept/convergence-versus-consensus-crdts-and-the-quest-for-distributed-consistency))
-   Shapiro et al.’s [comprehensive survey](https://hal.inria.fr/inria-00555588/document)
-   Attiya et al.’s [formal specification of collaborative text editing](http://software.imdea.org/~gotsman/papers/editing-podc16.pdf)
-   Gomes et al.’s [formal verification of CRDTs](https://dl.acm.org/citation.cfm?doid=3152284.3133933)

Projects
- [Automerge](https://automerge.org/)