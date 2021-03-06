# Word vectors: Sentiment classification
We will use word vector representations to build an Emojifier that classifies the sentiment of a sentence to one of a given number of classes and pick an emoji accordingly.
π€© π« π₯

An emojifier will make your text messages more expressive. Rather than writing:
> Congratulations on the promotion! Let's get coffee and talk. Love you!  

An emojifier can automatically turn this into:
> Congratulations on the promotion! π  Let's get coffee and talk. βοΈ Love you! β€οΈ

We implement a model that inputs a sentence (such as "Let's go see the baseball game tonight!") and finds the most appropriate emoji to be used with this sentence (βΎοΈ).

I did this project in the [Sequence Models](https://www.coursera.org/learn/nlp-sequence-models) course as part of the [Deep Learning Specialization](https://www.coursera.org/specializations/deep-learning).

## Dataset
We have a small training dataset (X, Y) where:
- X contains 127 sentences (strings).
- Y contains an integer label between 0 and 4 corresponding to an emoji for each sentence.

The test dataset contains 56 examples. Some examples of sentences and their labels (emojis) are shown below.

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

## Results

Some results from the baseline model are:
```
i adore you β€οΈ
i love you β€οΈ
funny lol π
lets play with a ball βΎ
food is ready π΄
not feeling happy π
```

The baseline model ignores word ordering and as a result don't do well on a phrase like:
>not feeling happy

The LSTM model gets this example right, but does not do well on some other examples:
```
Expected emoji:π prediction: he got a very nice raise	β€οΈ
Expected emoji:π prediction: she got me a nice present	β€οΈ
Expected emoji:π prediction: This girl is messing with me	β€οΈ
Expected emoji:π΄ prediction: any suggestions for dinner	π
Expected emoji:π prediction: you brighten my day	β€οΈ
Expected emoji:π prediction: she is a bully	β€οΈ
Expected emoji:π prediction: she said yes	π
Expected emoji:π΄ prediction: I did not have breakfast π
```
This is because the training set is small. If the training set were larger, the LSTM model would be much better than the baseline model at understanding more complex sentences.


