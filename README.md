# BWNLTK
## Billy Wu's natural language processing kit 

Using Google's word2vec algorithm, the BWNLTK will construct a variety of the state of art NLP models. The current tool kit will include a word2vec model constructor, an single word sentiment prediction model, a key word suggestion model, a sentence chunking engine, a CRF based NER engine, and eventually an actionability detection system.

### I.   Word2vec Model Constructor
The training data includes the WMT13 news data. Available languages will include English, Spanish, French, Russian, and German. The script will include a preprocess method and a model trainer with the following parameters: the vector dimension being 300, the window size for cbow/sg being 10, the number of threads being 4, and the minimum number of words appearance being 5
### II.  Single Words Sentiment Prediction System
..*  a. training set includes a list of words and their corresponding sentiments
..*  b. a word2vec model produced by the word2vec model constructor 
..*  c. a feature filter was constructed
..*  d. a list of svm models is then constructed based on filtered word vectors to improve the prediction precision
### III. Key Word Suggestion Model
..*  a. By doing basic vector arithematic, a word sense disambiguation mechanism is used to calculate the word-sense vector
..*  b. Using the previous word2vec model to suggest the most similar words aroud a given word-sense vector
### IV.  Sentence Chunking Engine
..*  a. This sentence chunking engine is based on word similarities and the amount of surprise calculated from word2vec
..*  b. A similarity median is established to be the cutoff along with some exception rules in case that a word appeared to be without a word2vec vector representation
### V.   CRF Based NER Engine
..*  a. Training set includes the conll2003 data
..*  b. A basic CRF model is constructed from python's crfsuite library
..*  c. A list of features:

  
