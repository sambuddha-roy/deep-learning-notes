### [Limited Discrepancy Beam Search](https://www.ijcai.org/Proceedings/05/Papers/0596.pdf)
#### Authors: David Furcy, Sven Koenig.

* What is Beam Search?

Consider a search tree, say a BFS search tree. We may not be able to explore all the nodes 
(because of time as well as memory/space considerations). Beam search aims to explore 
_only_ a few of the nodes at any _layer_ of the tree. 

* How do we choose which nodes to explore?

According to a _heuristic_ function that gives a _value_ to each node. 

