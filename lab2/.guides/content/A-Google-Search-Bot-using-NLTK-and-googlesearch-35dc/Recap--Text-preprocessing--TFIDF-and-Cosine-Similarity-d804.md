In the next part, we want to process this text to find the most similar sentence to each user input.

At this point, you must be familiar with some of the NLP concepts that we'll use in this lab. Let's review them:

### 1. Text preprocessing

- Tokenization takes raw text and generates a list of word or sentence tokens.
- Lemmatization reduces words to their most basic meaning. 
- It will give us a word that represents a grouping of words (e.g., the lemma of the word “every” is still "every".). 

### 2. TF-IDF

- Term Frequency-Inverse Document Frequency (TF-IDF) is sometimes referred to as “weighted” bag of words.
- TF-IDF rescales the frequency of words by how often they appear in all documents, so that the scores for frequent words like “the” that are also frequent across all documents are penalized.

### 3. Cosine Similarity

- If Euclidean distance is the straight line distance between vectors, Cosine similarity is the angular distance between vectors:

![.guides/img/cosine](.guides/img/cosine.png)

The formula is:

$$ cos(\theta) = \frac{A \cdot B}{||x|| * ||y||} = \frac{\sum_{i=1}^{n} A_iB_i}{ \sqrt{\sum_{i=1}^{n} A^2_i} \sqrt{\sum_{i=1}^{n} B^2_i}}$$

{Check It!|assessment}(multiple-choice-808691343)
