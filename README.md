# BiConvBERT

## Our Vision
- train a bilingual ConvBERT language model for German and English language
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
