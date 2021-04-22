# BiConvBERT

## Our Vision
- train a bilingual ConvBERT language model for German and English language - the advantage of such a builingual model is that you can mix free english datasets into your downsteam training to improve performance
- model size should be "medium" - somewhere between base and large - we will interpolate the parameters
- use a large and clean vocab so words are split into less tokens for faster prediction performance
- use lower-case tokenizer but keep accents (umlauts)
- do the training on GPUs instead of TPUs
- open-source it like [german-nlp-group/electra-base-german-uncased](https://huggingface.co/german-nlp-group/electra-base-german-uncased)

## Progress / News
- **2021-04-12:** hyperparameter planning for medium models started - see below
- **2021-04-02:** we open a PR for ConvBERT to be able to keep accents: [Add toggle to turn off `strip_accents`.](https://github.com/yitu-opensource/ConvBert/pull/17)

## Links
- [ConvBERT Paper](https://arxiv.org/abs/2008.02496)
- [ConvBERT GitHub](https://github.com/yitu-opensource/ConvBert)

## Impediments
- we have credits for GPUs but ConvBERT has to be trained on TPUs
- it might bring up problems when we train on multiple GPUs - see here https://github.com/yitu-opensource/ConvBert/issues/18

## Paper with Bilingual Approaches 
| Title                                                        | Languages        | Dataset size & split                                | Result                                                       | Links                                                        |
| ------------------------------------------------------------ | ---------------- | --------------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| GigaBERT: A Bilingual BERT for English and Arabic            | English & Arabic | Multiple Versions: largest: 6.1B (en) vs 4.3 B (ar) | Outperforms mBERT (no suprise as larger Data is used at Gigabert) and XLM-Rbase (this is an indicator that bilingual is superior to a multilingual) | https://arxiv.org/pdf/2004.14519v2.pdf                       |
| Towards Fully Bilingual Deep Language Modeling               | English & Finish | 3.8 B Tokens (en) & 3.3 B Tokens (finish())         | Outperforms mBERT (92.34 vs 88.88)                           | https://arxiv.org/pdf/2010.11639.pdf                         |
| Cross-Lingual Ability of Multilingual BERT: An Empirical Study |                  |                                                     | Couldn't draw a real concusion                               | https://openreview.net/pdf/1499e19238fd9d7ee8a9c7e7bb6f9e2c9e6a0adf.pdf |

## Datasets
- German Dataset
  - Cleaned German CC from Philipp Reissel
- English
  - Google C4 (colossal cleaned common crawl): https://www.tensorflow.org/datasets/catalog/c4
  - C4 download without preprocessing: https://github.com/allenai/allennlp/discussions/5056

## Training Runs
| Run      | Ressources Neede (GPU Hours) | Dataset size & split                  | Eval Datasets | Results / Conclusions |
| -------- | ---------------------------- | ------------------------------------- | ------------- | --------------------- |
| ConvBERT | ???                          | 50/50: 100 GB German / 100 GB English |               |                       |
|          |                              |                                       |               |                       |

## To-do
- [x] add ["strip_accents" PR from Electra](https://github.com/google-research/electra/pull/88) to ConvBERT
- [ ] clarify multi GPU training - https://github.com/yitu-opensource/ConvBert/issues/18
- [ ] select and preprocess German corpus
- [ ] select and preprocess English corpus
- [ ] prepare vocab
- [ ] train a small model for testing

## Hyperparameter
Hyperparameter | Small | Base | Large | Medium
---------------|-------|------|-------|-------
Number of layers | 12 | 12 | 24 | 18
Hidden Size | 256 | 768 | 1024 | 896
FFN inner hidden size | 1024 | 3072 | 4096 | 3584
Attention heads | 4 | 12 | 16 | 14
Attention head size | 64 | 64 | 64 | 64
Embedding Size | 128 | 768 | 1024 | 896
Generator Size | 1/4 | 1/3 | 1/4 | ?
Mask percent | 15 | 15 | 25 | ?
Learning Rate Decay | Linear | Linear | Linear | Linear
Warmup steps | 10000 | 10000 | 10000 | 10000
Learning Rate | 5e-4 | 2e-4 | 2e-4 | 2e-4
Adam epsilon | 1e-6 | 1e-6 | 1e-6 | 1e-6
Adam beta_1 | 0.9 | 0.9 | 0.9 | 0.9
Adam beta_2 | 0.999 | 0.999 | 0.999 | 0.999
Attention Dropout | 0.1 | 0.1 | 0.1 | 0.1
Dropout | 0.1 | 0.1 | 0.1 | 0.1
Weight Decay | 0.01 | 0.01 | 0.01 | 0.1
Batch Size | 128 | 256 | 2048 | ?
Train Steps (BERT/ELECTRA) | 1.45M/1M | 1M/766K | 464K/400K | ?
