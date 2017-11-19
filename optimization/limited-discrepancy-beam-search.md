### [Limited Discrepancy Beam Search](https://www.ijcai.org/Proceedings/05/Papers/0596.pdf)
#### Authors: David Furcy, Sven Koenig.

* What is Beam Search?


Consider a search tree, say a BFS search tree. We may not be able to explore all the nodes 
(because of time as well as memory/space considerations). Beam search aims to explore 
_only_ a few of the nodes (and this is called the _beam_) at any _layer_ of the tree. 


* How do we choose which nodes to explore, in a specific layer and which ones to discard?


According to a _heuristic_ function that gives a _value_ to each node. We sort the nodes in 
a layer by the heuristic value, and pick up the top-k (where k is the size the beam that we 
decide to go with).


* So beam search may be faster, with a smaller memory footprint. Where/when does it fail?


If the heuristic function is not necessarily a good guide, then beam search might never end 
up reaching the goal state.


* We want to retain the _flavor_ of beam search, but we also want to cover more states (so as 
to possibly reach the goal state). How do we do this?


_Backtracking_ is the popular answer. The paper first discusses _chronological_ backtracking, where
the nodes/states backtracked to are the ones that we _just came from_. 


* What is a problem with _chronological backtracking_?


The nodes/states backtracked to are the ones that we just came from recently. But the actual 
mistake (in having chosen wrong heuristic function, etc.) might have occurred much higher up in the 
tree, close to the root. 

This argument is reminiscent of the corresponding arguments in neural networks - that the weights of the 
first few layers are more important, and harder to change (because of vanishing gradients etc. in 
the backpropagation step).  

