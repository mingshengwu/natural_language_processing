# BWNLTK
## Billy Wu's natural language processing kit 

Using Google's word2vec algorithm, the BWNLTK will construct a variety of the state of art NLP models. The current tool kit will include a word2vec model constructor, an single word sentiment prediction model, a key word suggestion model, a sentence chunking engine, a CRF based NER engine, and eventually an actionability detection system.

### I.   Word2vec Model Constructor
The training data includes the WMT13 news data. Available languages will include English, Spanish, French, Russian, and German. The script will include a preprocess method and a model trainer with the following parameters. The vector dimension is determined to be 300 by default. The window size for cbow/sg is 10, the size of context to be taken into consideration. The number of threads is determined to be 4 to suit my own machine. The minimum frequency of the words that are included in   5
### II.  Single Words Sentiment Prediction System
The training set includes a list of words and their corresponding sentiments. Then a word2vec model produced by the word2vec model constructor is used to generate the potential features used to predict their sentiment. A feature filter was then constructed based on the correlation between each column of the training features and the annotated sentiment. Finally, a list of svm models is constructed on different subset of the entire training set rather than a single model based on the entire training set to improve the system's overall precision.
### III. Key Word Suggestion Model
By doing basic vector arithematic, a word sense disambiguation mechanism is used to calculate the word-sense vector。 Using the previous word2vec model, one can suggest the most similar words aroud a given word-sense vector related to a given topic.
### IV.  Sentence Chunking Engine
This sentence chunking engine is based on word similarities and the amount of surprise calculated from word2vec. A similarity median is established to be the cutoff along with some exception rules in case that a word appeared to be without a word2vec vector representation or the word happens to be a stop word.
### V.   CRF Based NER Engine
Training set includes the conll2003 data. A basic CRF model is constructed from python's crfsuite library. A list of features will include.

  
