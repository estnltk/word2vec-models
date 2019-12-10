# word2vec-models
Word2vec models trained on an estonian text corpus.

### Models
We provide a number of models trained with [word2vec](https://code.google.com/p/word2vec/) software. 
As training data, we used [Estonian Reference Corpus](http://www.cl.ut.ee/korpused/segakorpus/index.php?lang=en), a collection of texts covering newspaper, fiction, science and legislation domain.
We include separate models trained on the original and the lemmatised version of the corpus.

### Download
* Model files are available for download at [entu.keeleressursid.ee](https://entu.keeleressursid.ee/shared/7540/I7G5aC1YgdInohMJjUhi1d5e4jLdhQerZ4ikezz1JEv3B9yuJt9KiPl9lrS87Yz0).
* Earlier in time the same files were hosted at [ats.cs.ut.ee](http://ats.cs.ut.ee/keeletehnoloogia/estnltk/word2vec/).



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
>>> from gensim.models import KeyedVectors
>>> model = KeyedVectors.load_word2vec_format('lemmas.cbow.s200.w2v.bin', binary=True)
>>> model.most_similar('harjumaa')
[('lääne-virumaa', 0.7403180003166199),
 ('järvamaa', 0.7391915321350098),
 ('tartumaa', 0.7278606295585632),
 ('pärnumaa', 0.7234846949577332),
 ('viljandimaa', 0.7169549465179443),
 ('ida-virumaa', 0.7112703919410706),
 ('raplamaa', 0.6816533803939819),
 ('läänemaa', 0.6799672842025757),
 ('jõgevamaa', 0.6791231632232666),
 ('põlvamaa', 0.6766212582588196)]

```
For more details, refer to gensim documentation https://radimrehurek.com/gensim/models/word2vec.html
