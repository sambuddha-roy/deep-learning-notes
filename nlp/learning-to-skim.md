### [Learning to Skim Text](http://www.cs.cmu.edu/~weiyu/Adams_Wei_Yu_Homepage_files/acl17cr.pdf)
#### Authors: Adams Wei Yu, Hongrae Lee, Quoc V. Le

#####Basic Idea:

We want to _speed up_ how a machine reads a text. The goal is
to speed up classification tasks (such as, say, sentiment
analysis).

- **Thought 1**:
Allow the machine to _skim_ over the
text. What this means is that while an usual LSTM/RNN
has to go through the entire text, while maintaining
the _hidden state_, we are allowing the machine here to 
_jump_ over the text. 
- **Thought 2**:
Not every word in the text/document is created equal, not
all of them are important. By allowing _jumps_ we are 
essentially encouraging the machine to learn _more relevant_
words from the text. 
(I wonder if we can think of this as learning the _keywords_).

For skimming, we have to specify a few more parameters. Thus, the paper considers
parameters for

1. the number of jumps allowed
2. the max-length of any one jump
3. the number of tokens read between two jumps

##### Training:
- train a LSTM
- usual: 
    - will have the hidden state. 
    - also will have
the inputs as word embeddings that we will train. 
i.e. start with a word embedding initialization, 
flow through the networks, find out (extent of) error, 
backpropagate to change the embeddings. so far, usual
stuff. 
- unusual: how do we train the jumps? jumps are discrete (i.e. jump either
3 words, or 4 words, etc.). how do we backtrack from a 
_mistake_ here? in short, this is non-differentiable.
- training by sampling. have _multiple_ runs (a _jumping
action sequence_), and see how the specific task performs
(say, a classification task or so).
- step 1: discrete --> distribution. Learning something
discrete is hard (because of non-differentiability), so 
make it _smooth_ by learning a _distribution_ instead 
(remember LDA for topic modeling?)
    - we will sample the jump
 from a multinomial distribution.
    - the distribution will have _jump action parameters_.
    these will be conditioned on the hidden state so far
    (after seeing words according to the jump sequence so 
    far).
- step 2: feedback? so we set up the model of how we 
will have the jump action parameters, but how do we get
feedback to change it or not?
    - enter reinforcement learning.
    - given a sequence of actions, receive _reward_ as to 
    whether this sequence is relevant to learning or not.
    - expected reward over a sampled sequence of jumps
     (sampled according to the conditional distribution)
     is our objective function. 
- step 3: optimization. expectations are hard to optimize, 
so sample and estimate.

#####**A Toy Problem**
We are given a permutation
of the numbers (0, 1,..., n-1) and the function that we
are trying to learn is f(p) = p[p[0]].

For example, let p = [4, 3, 1, 2, 0] (for n = 5), and 
f(p) = p[p[0]] = 0.

Essentially, the first entry of the array indicates how 
much of a _jump_ we need to take in order to find the 
answer.

