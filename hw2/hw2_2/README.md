# MLDS2018SPRING/hw2/hw2_2
# 0. Requirements
```
tensorflow-gpu==1.6.0
numpy==1.14.2
pandas==0.22.0
gensim==3.4.0
```
# 1. Bulid word-based dictonary
Bulid word-based dictonary with min_count=20 and add TA's vocab.
```
python3 build_filter_words.py ./clr_conversation.txt ./vocab.txt ./word_vocab.txt
```
# 2. Filter training data with unknown token.
```
python3 filter.py ./clr_conversation.txt ./word_vocab.txt ./filtered_clr_conversation.txt
```
# 3. Data Preprocessing
Preprocessing on filtered training data.
```
python3 data_preprocessing.py ./filtered_clr_conversation.txt ./word_vocab.txt ./w2v_corpus.txt
```
# 4. Pre-train Word2Vec Model
Pre-train Word2Vec model with size 256, window 5, iteration 300.
```
python3 train_w2v.py ./w2v_corpus.txt ./w2vModel_256_w5_mc1_iter300.bin
```
# 5. Train Seq2Seq Model
```
rm ./models/*
python3 train.py
```
# 6. Inference on Testing Set
```
python3 infer.py ./test_input.txt ./test_output.txt
```
If you just wanna infer without training, please run hw2_seq2seq.sh.
```
bash ./hw2_seq2seq.sh ./test_input.txt ./test_output.txt
```
# 7. Evaluate Perplexity And Correlation Score
Please download TA's baseline model before evaluate our model.
```
cd mlds_hw2_2_data/evaluation
python3 main.py ../../test_input.txt ../../test_output.txt
```
# 8. Performance 
| Method                       | BLEU@1   |
| ---------------------------- |:--------:|
| Without Attention            | 0.7010   |
| Luong Attention              | 0.7054   |
| Luong Attention with scale   | 0.6977   |
| Bahdanau Attention           | 0.6965   |
| Bahdanau Attention with norm | 0.7204   |