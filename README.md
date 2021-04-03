# BiConvBERT

## Our Vision
- train a bilingual ConvBERT language model for German and English language - the advantage of such a builingual model is that you can mix free english datasets into your downsteam training to improve performance
- model size should be "medium" - somewhere between base and large - we will interpolate the parameters
- use a large and clean vocab so words are split into less tokens for faster prediction performance
- use lower-case tokenizer but keep accents (umlauts)
- do the training on GPUs instead of TPUs
- open-source it like [german-nlp-group/electra-base-german-uncased](https://huggingface.co/german-nlp-group/electra-base-german-uncased)

## Links
- [ConvBERT Paper](https://arxiv.org/abs/2008.02496)
- [ConvBERT GitHub](https://github.com/yitu-opensource/ConvBert)

## Impediments
- we have credits for GPUs but ConvBERT has to be trained on TPUs

## Datasets
- German Dataset
  - Cleaned German CC from Philipp Reissel
- English
  - Google C4 (colossal cleaned common crawl): https://www.tensorflow.org/datasets/catalog/c4

## To-do
- [ ] add ["strip_accents" PR from Electra](https://github.com/google-research/electra/pull/88) to ConvBERT
- [ ] select and preprocess German corpus
- [ ] select and preprocess English corpus
- [ ] prepare vocab

## Progress / News
- **2021-04-02:** we add a PR for ConvBERT to be able to keep accents: [Add toggle to turn off `strip_accents`.](https://github.com/yitu-opensource/ConvBert/pull/17)
