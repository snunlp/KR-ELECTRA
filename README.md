## KoRean based ELECTRA (KR-ELECTRA)

This is a release of a Korean-specific ELECTRA model with comparable or better performances developed by the Computational Linguistics Lab at Seoul National University. Our model shows remarkable performances on tasks related to informal texts such as review documents, while still showing comparable results on other kinds of tasks. 

### Released Model
We pre-trained our KR-ELECTRA model following a base-scale model of [ELECTRA](https://github.com/google-research/electra). We trained the model based on Tensorflow-v1 using a v3-8 TPU of Google Cloud Platform.

#### Model Details

We followed the training parameters of the base-scale model of [ELECTRA](https://github.com/google-research/electra).

##### Hyperparameters

|  model  | # of layers | embedding size | hidden size | # of heads |
| ------: | ----------: | -------------: | ----------: | ---------: |
| Discriminator | 12 | 768 | 768 | 12 |
| Generator | 12 | 768 | 256 | 4 |


##### Pretraining

| batch size | train steps | learning rates | max sequence length | generator size |
| ---------: | ----------: | -------------: | ------------------: | -------------: |
| 256 | 700000 | 2e-4 | 128 | 0.33333 |


#### Training Dataset

34GB Korean texts including Wikipedia documents, news articles, legal texts, news comments, product reviews, and so on. These texts are balanced, consisting of the same ratios of written and spoken data.


#### Vocabulary

vocab size 30,000
We used morpheme-based unit tokens for our vocabulary based on the [Mecab-Ko](https://bitbucket.org/eunjeon/mecab-ko-dic/src/master/) morpheme analyzer.


#### Download Link

* Tensorflow-v1 model ([download](https://drive.google.com/file/d/1L_yKEDaXM_yDLwHm5QrXAncQZiMN3BBU/view?usp=sharing))

* PyTorch models on HuggingFace

```
from transformers import ElectraModel, ElectraTokenizer

model = ElectraModel.from_pretrained("snunlp/KR-ELECTRA-discriminator")
tokenizer = ElectraTokenizer.from_pretrained("snunlp/KR-ELECTRA-discriminator")
```


### Finetuning

We used and slightly edited the finetuning codes from [KoELECTRA](https://github.com/monologg/KoELECTRA), with additionally adjusted hyperparameters. You can download the codes and config files that we used for our model. 


#### Experimental Results

|                       | **NSMC**<br/>(acc) | **Naver NER**<br/>(F1) | **PAWS**<br/>(acc) | **KorNLI**<br/>(acc) | **KorSTS**<br/>(spearman) | **Question Pair**<br/>(acc) | **KorQuaD (Dev)**<br/>(EM/F1) | **Korean-Hate-Speech (Dev)**<br/>(F1) |
| :-------------------- | :----------------: | :--------------------: | :----------------: | :------------------: | :-----------------------: | :-------------------------: | :---------------------------: | :-----------------------------------: |
| KoBERT                |       89.59        |         87.92          |       81.25        |        79.62         |           81.59           |            94.85            |         51.75 / 79.15         |                 66.21                 |
| XLM-Roberta-Base      |       89.03        |         86.65          |       82.80        |        80.23         |           78.45           |            93.80            |         64.70 / 88.94         |                 64.06                 |
| HanBERT               |       90.06        |         87.70          |       82.95        |        80.32         |           82.73           |            94.72            |         78.74 / 92.02         |               **68.32**               |
| KoELECTRA-Base        |       90.33        |         87.18          |       81.70        |        80.64         |           82.00           |            93.54            |         60.86 / 89.28         |                 66.09                 |
| KoELECTRA-Base-v2     |       89.56        |         87.16          |       80.70        |        80.72         |           82.30           |            94.85            |         84.01 / 92.40         |                 67.45                 |
| KoELECTRA-Base-v3 |     90.63      |       **88.11**        |     **84.45**      |      82.24       |         **85.53**         |          95.25          |       84.83 / **93.45**       |                 67.61                 |
| **KR-ELECTRA (ours)** | **91.168** | 87.90 | 82.05 | **82.51** | 85.41 | **95.51** | **84.93** / 93.04 | **74.50** | 
  
The baseline results are brought from [KoELECTRA](https://github.com/monologg/KoELECTRA)'s.


### Citation
```bibtex
@misc{kr-electra,
  author = {Lee, Sangah and Hyopil Shin},
  title = {KR-ELECTRA: a KoRean-based ELECTRA model},
  year = {2022},
  publisher = {GitHub},
  journal = {GitHub repository},
  howpublished = {\url{https://github.com/snunlp/KR-ELECTRA}}
}
```
