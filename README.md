# Word vectors: Sentiment classification
We will use word vector representations to build an Emojifier that classifies the sentiment of a sentence to one of a given number of classes and pick an emoji accordingly.
🤩 💫 🔥

An emojifier will make your text messages more expressive?
Rather than writing:
> Congratulations on the promotion! Let's get coffee and talk. Love you!  

The emojifier can automatically turn this into:
> Congratulations on the promotion! 👍  Let's get coffee and talk. ☕️ Love you! ❤️

We implement a model that inputs a sentence (such as "Let's go see the baseball game tonight!") and finds the most appropriate emoji to be used with this sentence (⚾️).

## Dataset
We have a small dataset (X, Y) where:
- X contains 127 sentences (strings).
- Y contains an integer label between 0 and 4 corresponding to an emoji for each sentence.

Some examples of sentences and their labels (emojis) are shown below.

![dataset](images/data_set.png)

Therefore, this is a classification problem with 5 classes.

## Models
We build two different models. With each model, we use the pre-trained 50-dimensional [GloVe](https://nlp.stanford.edu/projects/glove) as word embeddings.

### Baseline model
The baseline model simply averages the embeddings of the words in the input sentence, forward propagagetes the averge through a softmax layer.

![Baseline model](images/image_1.png)

In particular, this model does not consider the word ordering.

### LSTM model
The second model use LSTM to take word ordering into account.

![LSTM model](images/emojifier-v2.png)

