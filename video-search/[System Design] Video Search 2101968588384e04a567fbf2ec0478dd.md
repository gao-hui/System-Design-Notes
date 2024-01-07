# [System Design] Video Search

## High-level Design

![Untitled](%5BSystem%20Design%5D%20Video%20Search%202101968588384e04a567fbf2ec0478dd/Untitled.png)

## Text Processing

Text normalization: lowercaseing, punctuation removal, trim whitespace, Normalization Form KD (NFKD), strip accent, lemmatization and stemming

Tokenization: word tokenization, subword tokenization, character tokenization

Tokens to IDs: lookup table, hasing

![Untitled](%5BSystem%20Design%5D%20Video%20Search%202101968588384e04a567fbf2ec0478dd/Untitled%201.png)

## Text Encoder

Statistical methods:

- Bag of Words (BoW)
- Term Frequency Inverse Document Frerquence (TF-IDF)

ML-based Methods:

- Embedding layer
- Word2vec
- Transformer-based architectures (BERT, GPT3, BLOOM…)

## Video Processing

![Untitled](%5BSystem%20Design%5D%20Video%20Search%202101968588384e04a567fbf2ec0478dd/Untitled%202.png)

## Loss Computation

![Untitled](%5BSystem%20Design%5D%20Video%20Search%202101968588384e04a567fbf2ec0478dd/Untitled%203.png)

## Offline Metrics

- Precision@k and mAP
- Recall@k
- Mean Reciprocal Rank (MRR)

## Online Metrics

- CTR
- Videos completion rate
- Total watch time of search results

## Summary

![Untitled](%5BSystem%20Design%5D%20Video%20Search%202101968588384e04a567fbf2ec0478dd/Untitled%204.png)