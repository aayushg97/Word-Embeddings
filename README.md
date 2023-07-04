# Word-Embeddings

The large number of English words can make language-based applications daunting. To cope with this, it is helpful to have a clustering or embedding of these words, so that words with similar meanings are clustered together, or have embeddings that are close to one another.
But how can we get the meanings of words? John Firth (1957) put it thus:

`You shall know a word by the company it keeps.`

That is, words that tend to appear in similar contexts are likely to be related. This project will investigate this idea by coming up with an embedding of words that is based on co-occurrence statistics. This is done by following the steps below.

* Download the Brown corpus (using nltk.corpus). This is a collection of text samples from a wide range of sources, with a total of over a million words.
* Remove stopwords and punctuation, make everything lowercase, and count how often each word occurs. Use this to come up with two lists:
  * A vocabulary V , consisting of a few thousand (e.g., 5000) of the most commonly-occurring words.
  * A shorter list C of at most 1000 of the most commonly-occurring words, which we shall call context words.
* For each word w ∈ V , and each occurrence of it in the text stream, look at the surrounding window of four words (two before, two after).
  $$w_1 \quad w_2 \quad w \quad w_3 \quad w_4$$
  Keep count of how often context words from C appear in these positions around word w. That is, for w ∈ V, c ∈ C, define

  <p align="center">n(w, c) =  of times c occurs in a window around w</p>

  Using these counts, construct the probability distribution Pr(c|w) of context words around w (for each w ∈ V ), as well as the overall distribution Pr(c) of context words. These are distributions over C.
* Represent each vocabulary item w by a |C|-dimensional vector $\phi(w)$, whose c’th coordinate is:
$$\phi_c(w) = max \left(0, log \frac{Pr(c|w)}{Pr(c)} \right)$$
This is known as the (positive) pointwise mutual information, and has been quite successful in work on word embeddings.

The steps above can be used to come up with a 100-dimensional representation of words.

### Nearest neighbor using embeddings

Below is a list of words and their nearest neighbors determined using cosine distance over embeddings computed from the steps mentioned above.
  
| Word | Nearest Neighbor |
| --- | --- |
| time | period |
| first | second |
| man | boy |
| must | might |
| years | days |
| state | local |
| day | week |
| great | major |
| house | room |
| small | little |
| part | role |
| school | college |
| hand | arm |
| new | modern |
| think | believe |
| fact | characteristic |
| something | anything |
| course | action |
| united | attached |
| high | higher |
| two | three |
| old | young |
| could | would |
| said | told |
| people | men |

### Clustering vocabulary using embeddings

Using the embeddings, the words in V were clustered into 100 groups. K-means algorithm was used for clustering because it is easy to implement and runs fast in practice. Following is a table of some coherent clusters returned by K-means over the embeddings:

| Cluster label | Words |
| --- | --- |
| 12 | ’law’, ’board’, ’court’, ’committee’, ’county’, ’trade’, ’press’, ’feed’, ’hospital’, ’park’, ’laws’, ’post’, ’affairs’, ’campaign’, ’judge’, ’governments’, ’official’, ’claims’, ’chairman’, ’employees’, ’officials’, ’agencies’, ’friendly’, ’courts’, ’agency’, ’entitled’, ’positions’, ’practices’, ’welfare’, ’vehicles’, ’boards’, ’supreme’, ’automobile’, ’hopes’, ’grant’, ’offices’, ’legislation’, 'taxes’, ’considerably’, ’resulting’, ’departments’, ’appointed’, ’prison’, ’regional’, ’colleges’, ’steady’, ’legislature’, ’authorities’, ’provisions’, ’authorized’, ’guide’, ’stores’, ’presently’, ’financing’, ’elected’, ’strictly’, ’grave’, ’universities’, ’confronted’, ’protected’, ’shock’, ’buying’, ’slave’, ’sovereign’, ’questioned’, ’jurisdiction’, ’specified’, ’convention’, ’shoot’, ’variables’, ’terror’, ’contracts’, ’advisory’, ’depression’, ’automobiles’, ’boating’, ’physics’, ’capitol’, ’panic’, ’garage’, ’legislators’, ’hospitals’, ’parks’, ’relating’, ’enforcement’, ’commissioner’ |
| 14 | ’two’, ’three’, ’later’, ’several’, ’four’, ’five’, ’six’, ’hundred’, ’ten’, ’earlier’, ’seven’, ’eight’, ’nine’, ’twenty’, ’fifty’, ’thirty’, ’fifteen’, ’60’, ’dozen’, ’twelve’, ’eleven’, ’300’, ’forty’, ’fourteen’, ’70’, ’400’, ’42’ |
| 30 | ’years’, ’days’, ’times’, ’feet’, ’past’, ’million’, ’minutes’, ’months’, ’hours’, ’miles’, ’weeks’, ’inches’ |
| 70 | ’man’, ’boy’, ’wife’, ’woman’, ’girl’ |
| 73 | ’time’, ’day’, ’year’, ’night’, ’week’, ’moment’, ’morning’, ’century’, ’late’, ’meeting’, ’fall’, ’summer’, ’evening’, ’month’, ’spring’, ’visit’, ’afternoon’, ’season’, ’winter’, ’train’, ’session’, ’chapter’, ’decade’ |
| 88 | ’would’, ’could’, ’may’, ’must’, ’might’, ’whether’, ’shall’, ’cannot’ |
