---
title: attention in a transformer
date: 01-02-25
feed: show
---

these are notes that im in the progress of putting together. the goal of these notes is to better understand the foundation of large language models and to gain a stronger understanding of the fundamentals of deep learning. 

this is a new field to me so im constantly learning. these notes are made to share what i've learned and shouldn't be taken as truth. there are way better resources!! [learn ML](https://www.becachet.com/note/learn-ml). 

i will continue to update these types of notes as i learn more about the field. 

---

Stanford lecture from Andrej Karpathy
Reviewing [Attention Is All You Need](https://arxiv.org/pdf/1706.03762)

Neural Networks before transformers processed text sequentially. This is very similar to how humans reads text but have issues: 
- They're much slower because they have to process one word at a time
- They can forget important information from earlier when processing long sequences

**Attention was a big breakthrough because it lets the model directly connect any word to any other word**
For example, "The cat sat on the mat because it was comfortable" the model needs to know it refers to cat. it is very inefficient to do this sequentially. With attention, the model recognizes that "it" is strongly correlated to "cat".

Attention brought: faster speeds, better understanding, scalability (easier to train larger texts), versatility (works well for many language tasks)

## Scaled Dot-Product Attention
Basic building block, a single attention mechanism
Three inputs: Queries (Q), Keys (K), and Values (V)
This is basically the one "reader" looking at the text in a specific way
### This is attention...
You find the dot product between the query and all keys of the text and this is like measuring similarity (higher the dot product, higher the similarity). This result is the *Attention score* to recognize how relevant each position is. 

\
$$Attention(Q,V,K) = softmax(\frac{QK^T}{\sqrt{d_k}})V$$

$$d_k$$ is the scale because without scaling, large values can push softmax into regions where gradients are too small (keeps values in reasonable range)

Note: Softmax function is used to turn a list of numbers into probabilities. In this case the list of numbers is the attention score (how related is the query to each key)

Process: 
1. Compute similarity score using dot product $$Q*K$$
2. Scale them (divide by $$\sqrt{d_k}$$ )
3. Apply softmax to convert scores to probabilities
4. Use these probabilities to weight the values (V)

## Multi-Head Attention
Uses multiple Scaled Dot-Product Attention blocks in parallel 
- Gathers different "views" from each "reader" of the text
- Instead of one attention with full dimensionality, it creates h parallel heads 
- Each head has its own learned projections  for Q, K, and V
The whole purpose of this is to have multiple heads look at the text from a different perspective. 

## Query, Key, Value (QKV)
**Pretend you're searching through a library:**
Query (Q): What you're looking for (search terms)
Key (K): The index cards or catalog entries you're matching against
Value (V): The actual books/content you retrieve

**In the context of language processing:**
5. Query is the word/position you're currently focusing on
6. Key is all the words/positions you can potentially pay attention to
7. Value is the actual information you want to gather from those positions

---
more underway...