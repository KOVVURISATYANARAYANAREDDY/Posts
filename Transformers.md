
<h1 align="center"> Transformers </h1>
</br>

Natural Language Processing helped in dealing with many Machine Learning tasks that are required to Understand the Human Language. There are many Tasks that NLP can be used for such as Spam Classifier, Sentiment analysis, Language Translation, and many more. In past there were models that used TF-iDF vectors to represent the words that can be feed into Machine learning or Deep Learning Models. Later many embedding models came into existance where each word can be represented using a fixed set of continuous numbers to represent the words meaning. These Models performed well when compared to previous models. With these models a word can be represented only by fixed vector and cannot be changed in different contexts. So to answer this there are few models like ELMo, ULMFIT came into existance. But by using these and Convolution, recurrent networks, LSTMs achieved state-of-art results in Translation task. But due to some limitations like length of sentence to translate these models became worst as words that are apart very long are harder to detect their dependency. So in 2017 [***Attention is all you need***](https://arxiv.org/abs/1706.03762) paper Transformers were introduced. The Transformer – a model that uses attention to boost the speed with which these models can be trained. The Transformers outperforms the Google Neural Machine Translation model in specific tasks.

<p align = "center", width=100%>
  <img src="/Images/Transformers_architecture.jpg", height="550", width="650">
</p>

Translation is a task where one language sentence should be converted into another language.

Transformers are made up of encoder and decoder layers. Encoder layer contains a stack of encoders and Decoder layer contains a stack of decoders.
All these encoders are identical but do not share same weights. 
![encoder-decoder](https://user-images.githubusercontent.com/54667784/135790002-0bee65d6-2b42-49f0-82da-f1511ef259af.png)
