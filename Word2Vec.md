<h1 align='center'> Word2Vec </h1>

As for working with Text data we need to represent each word or document as a number or series on numbers word2vec is the choice.
A sequence of number can easily represent a word and can be good such that vector distances are less for words which are similar and large for words which are different.
We can find the similarity between word-vectors by using Cosine-Similarity.

![image](/Images/w2v-1.png)

Cosine-Similarity can be used for any length vectors.
We also called word-vectors as word-embeddings. There are few models that are trained for the purpose of Word-Embeddings such as GloVe. GloVe is trained on Wikipedia.
GloVe has various sizes of vectors for a same word.

![2](/Images/w2v-2.png)

Here if we compare “man” and “woman” are so close to each other than king.
**Analogies:**
We can add or subtract word-vectors to get another vector which can be closest to existing words. So that we can say by applying such transformations we can find similar word to that transformation.
A famous example is “King” – “Man” + “Women” = “Queen” .
A language model is trained on tasks like next word prediction. 
Words get their embedding by us looking at which other words they tend to appear next to.
1.	We get a lot of text data (say, all Wikipedia articles, for example). then
2.	We have a window (say, of three words) that we slide against all of that text.
3.	The sliding window generates training samples for our model.
When we start, the window is on the first three words of the sentence.
We take the first two words to be features, and the third word to be a label.

![3](/Images/w2v-3.png)

![4](/Images/w2v-4.png)

For memory efficiency purpose training happens while we slide the window.
Apart from neural network based approach previously N-gram was used for training language models.
Looking both ways.
Fill in the blank -> “Jay was hit by _” Bus,
But what if -> “Jay was hit by __ Bus”  red.
So here we can say not only previous words decide what this word is to be but words following this word also decides what exactly current word should be.
Continuous bag of Words.
Instead of looking two words before to determine the current word. We can also look at two words after it. This is called Continuous bag of words architecture.

![5](/Images/w2v-5.png)
![6](/Images/w2v-6.png)

Another architecture is skipgram.
Skipgram:
Instead of guessing a word using surrounding words like continuous bag of words. Skipgram tries to guess neighbouring words using current word.
![7](/Images/w2v-7.png)

Now to train a neural network to predict neighbour word. The model takes input word and try to predict target word. It will give probabilities for all words in vocabulary and top probable word is output as target word. And then we can get error, we transfer it backward.  

![8](/Images/w2v-8.png)

But this must be happened for every training example so that this is very computationally expensive. So, we can switch model task from predicting the neighbouring words to a task where, A model takes input word and output word and says whether they are neighbours or not (1 or 0).  So, this becomes very efficient in computational.

![9](/Images/w2v-9.png)

So, our input becomes two words and label is if they are neighbours or not.

![10](/Images/w2v-10.png)

But, now if we consider only examples where every datapoint is neighbours then model will simply output ‘1’ every time achieving 100% accuracy.
To handle this we can use “Negative Sampling” where we also take random words from vocab that are not neighbour to current word and label it as ‘0’.

![11](/Images/w2v-11.png)

Training:
For actual training we take two matrices – “Embedding Matrix” and “Context Matrix” each are having size (Vocab_size * embedding_size). while input word embedding is taken from Embedding Matrix and neighbouring word Embedding is taken from Context Matrix. We do dot product for these two vectors and get output by applying sigmoid. Calculate error and Update Model Parameters

![12](/Images/w2v-12.png)

At last we take Embedding Matrix and leave Context Matrix.
 
Hyperparameters:
Two hyperparameters in training process is “Window size” and “number of negative samples”. Better window size is 2-15. Gensim default window size is 5.

![13](/Images/w2v-13.png)

It states that 2-5 seems to be enough when you have a large enough dataset. The Gensim default is 5 negative samples.
