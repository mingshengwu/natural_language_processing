__author__ = 'Mingsheng Wu'

# to run word2vec fast version properly, one has to ensure that the machine has proper cmake, cython, and blas installed
# in addition, one has to ensure the proper version of scipy is installed since some versions of scipy has a deprecated
# version of blas.

from gensim.models.word2vec import Word2Vec,LineSentence
import re

import itertools, logging
logging.basicConfig(format='%(asctime)s : %(levelname)s : %(message)s', level=logging.INFO)

# preprocessing the word2vec training documents, removing all non-character symbols.
# preprocessed documents can be combined as well as saved in separate files.
# before running from this script, the input files are preprocessed so that the files are formatted one sentence per
# line.

# the option parameter allows the method to either return a list of preprocessed sentences as result or a simple boolean
# value with all the outputs written to a list of files. When the boolean option is used, the method expects output
# location as output_filename. If sentences option is selected, no destination location needs to be specified.

def single_file_preprocessing_en(input_filename,output_filename=None, return_option='sentence'):
    try:
        with open(input_filename) as f:
            content = f.readlines()
        sentences=[]
        for sentence in content:
            sentences.append(re.sub(r'[^\w]', ' ', sentence).replace("  "," "))
        if return_option=="boolean":
            f_out = open(output_filename, 'w')
            for item in sentences:
                f_out.write("%s\n" % item)
            return True
        else:
            return sentences
    except:
        return False

# the combined option allows one to specify if one wants the result not to be combined into one training file. If
# combined, one has to give a list of file names as output files with the same number of input file names.

def files_preprocessing_en(input_files,output_files,combined=True):
    if not combined:
        valid=True
        for input_filename,output_filename in itertools.izip(input_files,output_files):
            if not single_file_preprocessing_en(input_filename,output_filename,return_option="boolean"):
                print "File", input_filename, "failed to be transcribed into preprocessed format."
                valid=False
            else:
                print "File", input_filename, "was transcribed into preprocessed format."
    else:
        valid=True
        result=[]
        for input_filename in input_files:
            try:
                result+=single_file_preprocessing_en(input_filename,"None",return_option="sentences")
                print "File", input_filename, "was transcribed into preprocessed format."
            except:
                print "File", input_filename, "failed to be transcribed into preprocessed format."
                valid=False
        f_out = open(output_files[0], 'w')
        for item in result:
            f_out.write("%s\n" % item)
    if valid:
        print "All files were successfully processed."
    else:
        print "Not all files were successfully processed."
    return valid


# a method to build a word2vec model from a list of file names, but the vocabulary of the model is only taken from the
# first file
# the resulting model is saved to parameter model_name in the same directory as the working directory
def build_model_en(files, model_name):
    print "Model training started."
    if len(files)==1:
        sentences=LineSentence(files[0])
        model = Word2Vec(sentences, size=300, window=10, min_count=50, workers=4)
    else:
        first=True
        for file in files:
            sentences=LineSentence(file)
            if first:
                model = Word2Vec(sentences, size=300, window=10, min_count=10, workers=4)
            else:
                model.train(sentences)
    print "Model successfully built."
    model.save_word2vec_format(model_name,binary=True)
    return model


def test():
    try:
        print "Preprocessing started"
        result=files_preprocessing_en(['news-commentary-v10.en','news.2008.en.shuffled'],
                              ['en_training.txt'])
        print "Preprocessing finished"
        model=build_model_en(['en_training.txt'],'GoogleNews_EN.bin')
        #model = Word2Vec(sentences, size=300, window=10, min_count=5, workers=4)
        en_model_validating(model)
        return True
    except:
        return False


def en_model_validating(model):
    print model.most_similar("good",topn=50)
    print model.most_similar("Honda",topn=50)
    print model.most_similar("iphone",topn=50)
    print model.most_similar('computer',topn=50)
    print model.most_similar('hit',topn=50)
    print model.most_similar(['Chinese','river'])
    return 0



test()
