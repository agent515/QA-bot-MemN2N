# QA-bot-MemN2N 

This is an implementation (partial) of Facebook's baseline GRU/LSTM model on the bAbI dataset. The bAbI dataset contains 20 different question answering tasks. For the implementation, Single-supporting-fact set is used. 

Paper: [End to End Memory Networks: Sainbayar Sukhbaatar, Arthur Szlam, Jason Weston, Rob Fergus](https://arxiv.org/abs/1503.08895)

Dataset: [Facebook Research bAbI](https://research.fb.com/downloads/babi/)

<hr>

In order to give an answer based on the given text or sequence of text, it is important to understand the context of the whole story, giving emphasis to the key-words and relate each sentence with the previous sentences. LSTM (RNN) is used for storing this important information from previous result and using it along with new input to output new result.

### Architecture of the model:

![](/images/architecture.png)

To understand the architecture, reading the research paper mentioned above is highly recommended.

> **__NOTE__**: Original model concludes that hops increase the model's accuracy but implemented model doesn't implement the hops.

#### Training - Testing stats

![](/images/training_statistics.png)

Model achieves accuracy of **80%** while training and **75%** when testing.

####Example

QA-bot-MemN2N model takes *two* parameters as input: *story*, *question*
The vocabulary used to form input story and question must be subset of the vocabulary the model has been trained on.

Vocabulary, the model's been trained on:
{'.',
 '?',
 'Daniel',
 'John',
 'Mary',
 'Sandra',
 'Where',
 'back',
 'bathroom',
 'bedroom',
 'garden',
 'hallway',
 'is',
 'journeyed',
 'kitchen',
 'moved',
 'office',
 'the',
 'to',
 'travelled',
 'went'}

![](/images/input.png)

![](/images/output.png)

The model is 99.99% sure that the john is in the office.

Let's look at another example.

**story**: 
"Daniel journeyed to the Kitchen . John went to the bedroom . John travelled to the office . Daniel went to the garden . Sandra moved back to the Kitchen ."

**question**:
"Where is Daniel ?"

![](/images/input2.png)

![](/images/output2.png)

**There are cases where model got confused.**

With the same story in the previous example and question changed to "Where is John ?", model's output is different from the expected.

![](/images/input3.png)

![](/images/output3.png)

If we see, probability assigned to the output is very low.
Here's the top 5 answers predicted by the model based on the probabilities.

![](/images/output_probabilities.png)