---
layout: post
title: "Transformers"
categories: ml
excerpt: A post about the transformer neural network architectures
---

The transformer neural network model took the world by storm with the release of the GPT models.
They are much more successful than the earlier sequence-sequence neural network models such as RNNs and LSTMs because the transformer model can process multiple words in parallel, unlike the RNN based models. 
This speeds up the training process for transformers and allows it to handle larger datasets.  

There are a few core ingredients in the transformer neural network which I write about below, most of this I learnt from the [3blue1brown videos](https://www.youtube.com/playlist?list=PLZHQObOWTQDNU6R1_67000Dx_ZCJB-3pi) on the topic and by chatting with Claude.  



## Tokenization
Tokenisation is the process of converting words or word chunks into a  unit called tokens.
This is done via an algorithm such as Byte Pair Encoding (BPE), WordPiece, etc.  

The tokenisation algorithms are usually trained from a large corpus and are not learnable during the transformer’s training.
For BPE, we start with a single token per character; we then find pairs of tokens which are common in the text, merge them and create a new token out of it.
This process is repeated until we cannot find any more tokens.

The vocabulary size is limited to a fixed number of tokens.


## Embedding Matrix
The embedding matrix (which can be visualized as a large table) converts each of the tokens into a vector.
This matrix is learnable during the training process of the transformer.

The embedding matrix represents the token embeddings, i.e. the semantic meaning of the words.
These embeddings can be thought of as vectors in a high-dimensional space which preserve the word meanings
e.g. E(king) ~ E(queen) + E(man) - E(woman)


## Unembedding Matrix
It performs the reverse operation of the embedding matrix, i.e. it converts the vectors produced by the network back into our vocabulary.

This process is performed via the unembedding matrix aka the output embedding matrix or projection matrix.
The unembedding matrix is the transpose of the embedding matrix, this acts as a regularizer for the model and keeps the number of parameters low.  


## Attention Mechanism
The basic idea behind this mechanism is that the embedding for a particular word is updated by the surrounding words, which add context.
This mechanism can be visualized as the vector corresponding to the word embedding moving around in space after being updated by the surrounding words.
Its final position better reflects the meaning of the word.  

As an example, say that we have a sentence, "He created a miniature Eiffel tower lego model".
Initially, the vector embedding for the word 'tower' can be imagined to be at a point in space which represents the general conept of towers or skyscrapers.
Because of the word 'Eiffel' in the sentence, the embedding for the word 'tower' might be updated to a point in space which is associated with the Eiffel tower in particuar, and might be related to the embeddings for Paris, France, etc.
The word 'miniature' and 'lego' would then update the embedding for 'tower' to a point which better represents lego characters and toy models.
Note that this is a very hand-wavey example which aims to capture the general idea behind the attention mechanism.  

I will explore the technical details behind this mechanism as well as the remaining parts of the transformer model in a later post.
