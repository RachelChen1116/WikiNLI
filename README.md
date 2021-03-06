# Collection for WikiNLI Corpus

This is the code we used to collect WikiNLI corpus through implementation of pre-trained [Opus-MT](https://github.com/Helsinki-NLP/Opus-MT) models on the [WikiMatrix data](https://github.com/facebookresearch/LASER/tree/master/tasks/WikiMatrix).

## Data
We choose Indonesian, Czech, French, Japanese, German corpus from the WikiMatrix data, and create our corpus by sampling from the corpus with all the range of scores.

## Models
We use the [processor](https://github.com/RachelChen1116/WikiNLI/blob/master/preprocessor.py) in the Opus-MT framework to load the [Public MT-OPUS models](https://github.com/Helsinki-NLP/Opus-MT-train/tree/master/models) (including the [SentencePiece](https://github.com/google/sentencepiece)-based pre-processors and the models). The models translate the sentences on WikiMatrix into English based on the [Marian-NMT](https://marian-nmt.github.io/), where more command-line options can be found to change the setting of translation.

The [post-processor](https://github.com/RachelChen1116/WikiNLI/blob/master/postprocessor.py) resolves the encoding issues in the translation and filters out the sentence pairs that are detected as in other languages. The datasets are finally saved as csv files.

## Implementation
To implement the collection, run the [launch.sbatch.sh](https://github.com/RachelChen1116/WikiNLI/blob/master/launch.sbatch.sh) file with the language code. There are 5 languages that can be chosen from: Indonesian(id), Japanese(ja), French(fr), Czech(cs), German(de). For example:

```
chmod +x launch.sbatch.sh
./launch.sbatch.sh fr
```

## Evaluation
To get the evaluation of data, configure CoreNLP by following the [instructions](https://stanfordnlp.github.io/stanza/corenlp_client.html#usage) and start the client, then run the [evaluation.py](https://github.com/RachelChen1116/WikiNLI/blob/master/evaluation.py) file with the input as the json data file path to get the results.



## References

[1] Holger Schwenk, Vishrav Chaudhary, Shuo Sun, Hongyu Gong and Paco Guzman,
    [*WikiMatrix: Mining 135M Parallel Sentences in 1620 Language Pairs from Wikipedia*](https://arxiv.org/abs/1907.05791)
    arXiv, July 11  2019.

[2] Rico Sennrich, Barry Haddow and Alexandra Birch (2015). Neural Machine Translation of Rare Words with Subword Units.
	Proceedings of the 54th Annual Meeting of the Association for Computational Linguistics (ACL 2016). Berlin, Germany.