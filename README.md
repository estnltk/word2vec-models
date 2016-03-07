# word2vec-models
Word2vec models trained on an estonian text corpus.

### Models
We provide a number of models trained with [word2vec](https://code.google.com/p/word2vec/) software. 
As training data, we used [Estonian Reference Corpus](http://www.cl.ut.ee/korpused/segakorpus/index.php?lang=en), a collection of texts covering newspaper, fiction, science and legislation domain.
The models have been trained using both original and lemmatized version of the corpus.

Model's file name encodes a particular set of parameters used for training as `<CORPUS>.<ARCHITECTURE>.s<SIZE>.w2v.<FORMAT>`, where

CORPUS: lemmas or words  
ARCHITECTURE: sg (skip gram) or cbow (continuous bag of words)  
SIZE: word vector siz (100 or 200)
FORMAT: model format: bin (binary) or txt (text)  


### Download
Model files are available for download at http://ats.cs.ut.ee/keeletehnoloogia/estnltk/word2vec/

### Training Data
The corpus consists of 16M sentences, 55M words and 3M types. Lemmatized version of the corpus contains 2M types.
Corpus preprocesing, including tokenization and lemmatization, have been performed using `estnltk` toolkit.

### Usage
The models can be used with [word2vec](https://code.google.com/p/word2vec/) tools or [gensim](https://radimrehurek.com/gensim/).

*Word2vec* examples:
```bash
>./distance lemmas.cbow.s200.w2v.bin
Enter word or sentence (EXIT to break): harjumaa

Word: harjumaa  Position in vocabulary: 1376

                                              Word       Cosine distance
------------------------------------------------------------------------
                                          tartumaa              0.692018
                                       viljandimaa              0.636981
                                          pärnumaa              0.599145
                                          läänemaa              0.596758
                                          järvamaa              0.564394
                                         jõgevamaa              0.563559
                                          valgamaa              0.563454
                                               ...

```

```bash

>./word-analogy lemmas.cbow.s200.w2v.bin
Enter three words (EXIT to break): tallinn harjumaa tartu

Word: tallinn  Position in vocabulary: 43

Word: harjumaa  Position in vocabulary: 1376

Word: tartu  Position in vocabulary: 128

                                              Word              Distance
------------------------------------------------------------------------
                                          tartumaa              0.739888
                                         jõgevamaa              0.632034
                                       viljandimaa              0.623195
                                          valgamaa              0.599240
                                          järvamaa              0.598929
                                          pärnumaa              0.590916
                                          põlvamaa              0.584784
                                              võru              0.562844
                                               ...
```

*Gensim* example:
```python 
>>> from gensim.models import Word2Vec
>>> model = Word2Vec.load_word2vec_format('lemmas.cbow.s200.w2v.bin', binary=True)
>>> model.most_similar('harjumaa')
[(u'tartumaa', 0.6920183897018433),
 (u'viljandimaa', 0.6369808316230774),
 (u'pärnumaa', 0.5991454720497131),
 (u'läänemaa', 0.5967578887939453),
 (u'järvamaa', 0.5643939971923828),
 (u'jõgevamaa', 0.5635586977005005),
 (u'valgamaa', 0.5634534955024719),
 (u'tn1', 0.5596972703933716),
 (u'raplamaa', 0.5580025315284729),
 (u'põlvamaa', 0.547003448009491)]

```
For more details, refer to gensim documentation https://radimrehurek.com/gensim/models/word2vec.html
