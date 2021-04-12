# Word Embedding Techniques
<hr>

## Preparing Word for Word Embedding
### Tokenization
Helps to convert paragraphs to sentences or words

### Stemming and Lemmatization
Process of reducing words to their word stem

#### Stemming vs Lemmatization
Lemmatization is different from Stemming as Lemmatization helps to get the word as available in vocabulary , not just the word stem of it. <br>
It means that word that is understood by humans, will have its meaning.Lemmatization takes more time than stemming<br>

**Example**<br>
finally , final, finalized = Stemming (fina) / Lemmatization(final)

**Applications**
* Stemming can be used like Setiment Analysis, Spam Classification where we don't need to create a meaningful word<br>
* Lemmatization can be used like in Chatbots,Q&A where we need to sent repsonse and that needs meaningful word


## Word Embedding Techniques

### Bag of Words (Count Vectorizer) (Document Matrix)
A bag-of-words is a representation of text that describes the occurrence of words within a document.<br>
Words with their frequency and their respective matrix will be formed considering the sentences<br>
Those words will be written as features(f1,f2,f3) and will consider each sentence and give 1 in feature if the word exist in sentence and 0 if not
and this whole thing represented in a dataframe, meaning the vectors are created from words.

**Cons**<br>
In Bag of Words technique, we are not able to determine which word is more important, as when we create vector using this, it is either word is present(1) or not present(0)<br>
But in sentiment analysis, we want to give more value to positive or negative words

**We have better techniques than Bag of Words to create vectors like TF-IDF or Word2Vec**

### TF-IDF (Term Frequency - Inverse Document Frequency)
**Term Frequency** = No. of repetition of words in a sentence / No. of total words in a sentence  (single sentence)

eg--Sentence1 = good boy, Sentence 2= good boy girl <br>
* TF Matrix will be for Sentence1 (good) = 1/2 , boy = 1/2 girl = 0
* TF Matrix will be for Sentence2 (good) = 1/3 , boy = 1/3 girl = 1/3

**Inverse Document Frequency** - log(No. of Sentences / No. of sentences containing words)<br>
Here 2 is the no. of sentences being constant and next part is the no. of sentences containing the particular word<br>
* IDF Matrix will be good = log(2/2) = 0 , boy = log(2/2) = 0 , girl = log(2/1) = log2

Finally, we will multiply TF * IDF

**TF-IDF gives importance to uncommon words (There is a chance of overfitting)**<br>
**Both Bag of Words and TF-IDF, semantic information is not stored (semantic means orderwise data is not stored leading to no relation between the words in sequence)**


### Word2Vec
In this, each word is basically represented as a vector of 32 or more dimension instead of a single number<br>
Here the semantic information and relation between words is also preserved<br>

To use this, we need to install **"gensim" library** (install it)
* Gensim models creates a 100 dimension vector for each word specifing the relation with words

**In all the Above Techniques, Sequence Data is discarded**

### Using Embedding Layer (Keras)
If we apply One hot representation to a 10000 words dictionary, we will get 10000 dimension column for each word
eg--Man at 5000 index will be represented with [0,0,0,0,....0,0,1,0..,0]. Not storing any semantic information and also very hard for machine to train
**Sparse Matrix--This representation will become Sparse matrix--It means more no. of zeros and less no. of Ones

To solve this, we use Word Embedding (and specific technique named as Feature Representation)
For this, we have some features(predefined by us) and a 10000 words dictionary
Now in this dimension is reduced to 300 for each word, far better than one hot representation

<table>
<tr>
<th>Defined Features</th>
<th>Boy</th>
<th>Girl</th>
<th>King</th>
<th>Apple</th>
</tr>
<tr>
<td>Gender</td>
<td>-1</td>
<td>1</td>
<td>-1</td>
<td>0.1</td>
</tr>
<tr>
<td>Royal</td>
<td>0.01</td>
<td>0.02</td>
<td>0.95</td>
<td>0.01</td>
</tr>
<tr>
<td>Fruit</td>
<td>0.03</td>
<td>0.01</td>
<td>0.01</td>
<td>0.97</td>
</tr>
</table>


We can make analogy here, like if Boy tends to Girl, then what will king tends to ....<br>
We find the similarity between the words using Cosine Similarity(most used in Recommendation System)<br>
If we convert this 300 dimension matrix into 2 dimension, we will see that Boy and Girl are near, King and queen are near, Apple and Mango are near.
