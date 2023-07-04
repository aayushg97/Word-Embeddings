# Word-Embeddings

The large number of English words can make language-based applications daunting. To cope with this, it is helpful to have a clustering or embedding of these words, so that words with similar meanings are clustered together, or have embeddings that are close to one another.
But how can we get at the meanings of words? John Firth (1957) put it thus:

`You shall know a word by the company it keeps.`

That is, words that tend to appear in similar contexts are likely to be related. This project will investigate this idea by coming up with an embedding of words that is based on co-occurrence statistics. This is done by following the steps below.

* Download the Brown corpus (using nltk.corpus). This is a collection of text samples from a wide range of sources, with a total of over a million words.
* Remove stopwords and punctuation, make everything lowercase, and count how often each word occurs. Use this to come up with two lists:
** A vocabulary V , consisting of a few thousand (e.g., 5000) of the most commonly-occurring
words.
** A shorter list C of at most 1000 of the most commonly-occurring words, which we shall call
context words.
* For each word w ∈ V , and each occurrence of it in the text stream, look at the surrounding
window of four words (two before, two after). Keep count of how often context words from C appear in these positions around word w. That
is, for w ∈ V, c ∈ C, define
n(w, c) = # of times c occurs in a window around w.
Using these counts, construct the probability distribution Pr(c|w) of context words around w (for
each w ∈ V ), as well as the overall distribution Pr(c) of context words. These are distributions
over C.
* Represent each vocabulary item w by a |C|-dimensional vector Φ(w), whose c’th coordinate is:
Φc(w) = max 
0, log Pr(c|w)
Pr(c)

.
This is known as the (positive) pointwise mutual information, and has been quite successful in
work on word embeddings.
