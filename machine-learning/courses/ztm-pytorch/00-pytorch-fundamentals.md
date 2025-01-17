## Machine Learning vs Deep Learning

<br>

#### When to Use Machine Learning?

- When data is structured (spreadsheet, etc.).
- Examples of machine learning algorithms (shallow algorithms):
	- Random forest
	- Gradient boosted models
	- Naive Bayes
	- Nearest neighbor
	- Support vector machine
	- etc...

<br>

#### When to use Deep Learning?

- When data is not structured (website, voice, etc.).
- Example of deep learning algorithms:
	- Neural networks
	- Fully connect neural network
	- Convolutional neural network
	- Recurrent neural network
	- Transformers
	- etc...

<br>

---

<br>

## Anatomy Of Neural Networks (Basics)

<br>

**Input Layer**:
- Data that goes in

**Hidden Layer(s)**:
- Learns patterns in data
- Number of units/neurons vary

**Output Layer**:
- Outputs learned representation or prediction probabilities
- Number of units/neurons vary (?)

<br>

> NOTE: Each layer is usually a combination of linear (straight line) and/or non-linear (not-straight line) functions.
>
> NOTE: "Patterns" is an arbitrary term often referred to as "embedding", "weights", "feature representation", "feature vectors", etc. all referring to similar things.

<br>

---

<br>

## Different Types of Learning Paradigms

<br>

#### Supervised Learning

- Data (inputs / examples) and labels (identifying what the data is).

#### Unsupervised & Self-supervised Learning

- Data without labels.
- Learn patterns without knowing. 

#### Transfer Learning

- Take the patterns learned from one model to another model.

#### Reinforcement Learning

- Uses an environment with an agent.
- Example: 
	- **Environment**: situation where command is given
	- **Agent**: the dog
	- **Action**: the dog's response to the command (like sitting or not sitting)
	- **Reward**: The treat (reinforces the desired behavior)

<br>

---

<br>

## What Can Deep Learning Be Used For

<br>

#### Some Deep Learning Use Cases

- Recommendation system (YouTube, etc.)
- Language translation
- Speech recognition
- Computer vision
- Natural language processing (NLP)

<br>

> NOTE: Translation, speech recognition, etc. are examples of "Sequence to sequence (or seq2seq)".
>
> NOTE: Natural language process is an example of "Classification / regression".

<br>

---

<br>

## What Is and Why PyTorch

[PyTorch Documentation](https://pytorch.org/docs/stable/index.html)

#### What is PyTorch?

- Most popular research deep learning framework [trends](https://paperswithcode.com/trends)
- Write fast deep learning code in Python (able to run on GPU/many GPUs)
- Able to access many pre-build deep learning models (Torch Hub / torchvision.models)
- Whole stack: preprocessing data, model data, deploy model in your application / cloud
- Originally designed and used in-house by Facebook/meta (now open-sourced), Tesla, Microsoft, OpenAI

<br>

#### Why PyTorch?

- Research favorite
- Used practically everywhere AI is used
- Run code more effectively on GPU/TPU

<br>

---

<br>

## What are Tensors?

- A numerical representation of input data.

> "In mathematics, a tensor is an algebraic object that describes a multilinear relationship between sets of algebraic objects related to a vector space." - [Wikipedia](https://en.wikipedia.org/wiki/Tensor)

<br>

---

<br>

## What We Are Going To Cover With PyTorch

Now:

- PyTorch basics and fundamentals (dealing with tensors and tensor operations)

Later:

- Preprocessing data (getting it into tensors)
- Building and using pretrained deep learning models
- Fitting a model to the data (learning patterns)
- Making predictions with a model (using patterns)
- Evaluating model predictions
- Saving and loading models
- Using a trained model to make predictions on custom data

<br>

#### A PyTorch Workflow

1. Get data ready (turn into tensors)
2. Build or pick a pretrained model (to suit your problem)
	1. Pick a loss function & optimizer
	2. Build a training loop
3. Fit the model to the data and make a prediction
4. Evaluate the model
5. Improve through experimentation
6. Save and reload your trained model

<br>

---

<br>

