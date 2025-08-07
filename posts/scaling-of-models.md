---
title: scaling of language models
date: 20-02-25
feed: show
---

reading [Scaling Laws for Neural Language Models](https://arxiv.org/pdf/2001.08361)

Note: it would be smart to have a [[Neural Networks]] 101 page

# the purpose of this page:
im continuously trying to build my foundation of knowledge to better understand the structure of these new models as new information and methods seem to release every day. i was reading ["Scaling Laws for Neural Language Networks"](https://arxiv.org/pdf/2001.08361) paper to understand the importance of scaling laws. below are my quick notes on a flight, outlining my key takeaways. you will notice the naiveness in the beginning struggling to understand simple terms which seems to be common nomenclature in the industry. using local llms and reference papers i was able to gather a high level understanding of the implications from scaling laws. 

if you want to read my final consensus, jump to [Overall](#overall). 

note: i will probably add to this as you will see there are some big questions I don't know the answer to yet. 

---
## Understanding some key terms first: 
- **loss function:** the difference between predicted output of the model and true target value. common loss function is mean squared error (MSE) for regression tasks and cross-entropy for classification tasks
- **test loss:** calculated by applying the loss function to the predictions made on the test set and comparing them to the true labels. (lower test loss indicates better performance on unseen data)
- **convergence:** the point when an optimization algorithm approaches a stable solution where further iterations or updates no longer significantly change the parameters of the model. (model performance has been stabilized)
- **FLOPs:** "Floating Point Operations per Second" used to measure computational performance. 
	- single floating point operation is an arithmetic computation involving numbers with fractional parts. 
	- neural networks involve large amounts of floating-point arithmetic
- **overfitting:** this will decrease the models performance and occurs when the model begins to memorize the training data rather than generalizing from it. therefore, the model performs well on trained data but will perform poorly on new unseen data

## Largest principle discovered from scaling laws: 
- As the model scales in size (whether thats: compute, dataset size, or parameters) model performance improves smoothly
- performance has a power-law relationship with each individual facto when not bottlenecked by the other two

### What are hyperparameters? 
- settings that are determined before training begins and influence how the model learns from the data
- **depth:** refers to the number of layers it has
- **width:** number of neurons or nodes in each layer

*This scaling laws paper states that hyperparameters aren't nearly as significant in model performance as the size of the model itself*

Scaling laws in large language models prove that the most significant levers in model improvement are increasing the size of the model. the three parameters that can be scaled are: compute, dataset size, and number of parameters. these alone contribute much higher to the model's performance than other items such as hyperparameters. 

## 4. Infinite Data Limit and Overfitting
From Section 4 in "Scaling Laws of Neural Language Models"

The two parameters changing model performance in this senario is N (number of parameters) and D (Dataset size)
### Data Size Bottleneck
It is proven that for smaller datasets (D) as parameters (N) increase there is no improvement to model performance. Test loss begins to plateau. That means that there is risk in small dataset sizes when training models. Theres a strong correlation between N and D needing to increase together. 

For larger datasets (D), Test loss following a standard power law, model performance scales as predicted.

### Overfitting
Overfitting occurs most when dataset size (D) is low are parameters (N) are high. The model will naturally begin to memorize test information rather than generalizing from it making it inaccurate to unseen data. 

### Capacity Limitation
There is an inherit capacity limitation with fixed sized models that prevent it from achieving optimal performance. Beyond a certain point increasing N with D capped won't improve the model

There is technically a cap to the knowledge that can be used as D in any model (There is only so much information that exists in a digestible format right now). That means that with this capped dataset size, no matter the increase in model size, there will be little to no improvement. 

That begs the question about [[Reinforcement Learning]]. 
Theres more thinking that needs to be done here. I'm assuming that whether you use RL or not, it doesn't change the size of your dataset, but rather how you trained on it.


<h2 id="Overall">Overall</h2>

My current thought process is that there is a natural cap to the knowledge we can acquire right now. There are only so many websites and books that can be digested into a training set. Therefore, due to this natural cap, there is a natural limit to model performance. In the scaling laws paper is was stated that without a proportional increase the dataset size, there is no increase in model performance.

Does that mean we hit a plateau in model performance? Sure, we can continue to expand the quality of these datasets, and continue adding newer information, but this is not at the same logarithmic scale of growth we've been seeing from GPT-2 to GPT-4. 

My biggest question right now, is how can we jump over this hurdle of dataset capping? Will we need to generate artificial data and learn of of that? Does Reinforcement Learning play a role in this? These are these questions I'll need to find an answer to next...