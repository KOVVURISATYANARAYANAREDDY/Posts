
<h1 align="center"> Transformers </h1>
</br>

Natural Language Processing helped in dealing with many Machine Learning tasks that are required to Understand the Human Language. There are many Tasks that NLP can be used for such as Spam Classifier, Sentiment analysis, Language Translation, and many more. In past there were models that used TF-iDF vectors to represent the words that can be feed into Machine learning or Deep Learning Models. Later many embedding models came into existance where each word can be represented using a fixed set of continuous numbers to represent the words meaning. These Models performed well when compared to previous models. With these models a word can be represented only by fixed vector and cannot be changed in different contexts. So to answer this there are few models like ELMo, ULMFIT came into existance. But by using these and Convolution, recurrent networks, LSTMs achieved state-of-art results in Translation task. But due to some limitations like length of sentence to translate these models became worst as words that are apart very long are harder to detect their dependency. So in 2017 [***Attention is all you need***](https://arxiv.org/abs/1706.03762) paper Transformers were introduced. The Transformer – a model that uses attention to boost the speed with which these models can be trained. The Transformers outperforms the Google Neural Machine Translation model in specific tasks.

<p align = "center", width=100%>
  <img src="/Images/Transformers_architecture.jpg", height="550", width="650">
</p>

Translation is a task where one language sentence should be converted into another language.

Transformers are made up of encoder and decoder layers. Encoder layer contains a stack of encoders and Decoder layer contains a stack of decoders.
All these encoders are identical but do not share same weights. 

<p align = "center", width=100%>
  <img src="/Images/encoder-decoder.png", height="350", width="400">
</p>

An Encoder contains a Self-Attention layer and a Feed Forward layer. While a Decoder contains Masked Self-Attention layer, Encoder-Decoder Attention and a Feed Forward Layer.
![sub-layers](/Images/sub-layers.png)

### Transition of Input:
Firstly inputs for a Transformer must be tokens. A Token is a word or a piece of word. If you take a sentence then all words in it will be converted into tokens and then feed into Transformer. Each input token will be converted to an Embedding vector of size 512 from Embedding Matrix. So, the encoder receives list of vectors. This Embedding happens only at bottom most encoder while other encoders take output from previous encoders as input and no further embedding as Encoder layer is a stack of Encoders. The word in each position flows through its own path.
![Encoder-path](/Images/Encoder-path.png)

### Self-Attention layer 
A layer that helps the encoder look at other words in the input sentence as it encodes a specific word. The outputs of the self-attention layer are fed to a feed-forward neural network. The exact same feed-forward network is independently applied to each position.
But in decoder a separate “Encoder-Decoder Attention” layer which focus on relevant part of the input sequence.

Look at the sentence.
<p align = "center">
<b>“The animal didn’t cross the street because</b> <i>It</i> <b>was too tired”</b>
Here ‘it’ refers to Animal. 
</p>

<p align = "center">
<b>“The animal didn’t cross the street because</b> <i>It</i> <b>was too long”</b>
 Here ‘it’ refers to Street.
</p>

A Human can easily understand that But how can a machine understand. So, Self-Attention is used to understand the relevance of one word w.r.t other words.
![Self-Attention](/Images/Self-Attention.png)

Here each line from words to **it** represents how much each word influences **it**. We can identify **it** was more influenced by *animal* than *street*.

Firstly, we generate Query Vector, Key Vector, Value Vector by multiplying Embeddings of words with Query Matrix, Key Matrix, Value Matrix. Here embeddings size is 512 and each query, key, value vectors is 64, this is because we use **“Multiheaded attention”**. 
![qkv](/Images/qkv.png)

In the above figure words Thinking, Machines are first converted into Embedding Vectors X1, X2 respectively. Then by multiplying Weight matrices of Query, Key, Value with X1, X2 produces q1, q2, k1, k2, v1, v2.

Second step is to find scores. For calculating self-attention for “Thinking” we need to do dot product of query vector of “Thinking” with all key vectors of other words to get scores and apply softmax to get sum of all scores to 1. Then we multiply value vectors w.r.t their scores and sum them to get resulting vector (Z). This vector is then send to Feed Forward network.
![scores](/Images/scores.png)

This is for one attention but Transformers uses Multi-headed-Attentions(8 attention heads). But Why do we need multiple attentions, Because having only one head will make focus on few words neglecting other words so if we have multiple attentions different dependencies can be identified. Then we concat all outputs from different attentions and project to embedding size, which can further be processed by Feed Forward layer.

![All-in-self](/Images/All-in-self.png)

These Z vectors are individually processed by Feed Forward network. 
But still we miss something how can the model knows the position of each token while processing it in Encoder. Here comes **Positional Encoding** we add *Positional Encoding* for each word to its embedding. Positional Encoding just represents the position of each word.
![Adding-Position](/Images/Adding-Position.png)

In Encoders before sending output to further sub-layers we add input to output and normalize it. This can be understood from below figure.
![Residuals](/Images/Residuals.png)

## Decoder
