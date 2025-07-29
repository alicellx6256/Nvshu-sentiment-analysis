# Nvshu-sentiment-analysis
This is my final project for CS72 (Computational Linguistics). I collaborated with my classmate Youmi on this project.

## About the project: 
Nüshu is a unique, syllabic script historically used by women in Jiangyong County, China. As an endangered, low- resource writing system with limited digital resources, it presents a valuable case for evaluating sentiment classification in niche linguistic contexts. **This project tests four classification methods (fine-tuned BERT, Convolutional Neural Networks (CNN), Naïve Bayes, and Random Forest) on a manually labeled dataset of 500 Nüshu- Chinese sentence pairs. The goal was to assess which models best identify positive, neutral, and negative sentiment in a phonetic and culturally symbolic script.** CNN achieved the highest F1-score, while BERT performed the worst, likely due to domain mismatch and insufficient data. Overall accuracy remained below 65% across models. We identify contributing factors such as small dataset size, class imbalance, short sentence length, and semantic ambiguity. These results suggest that simpler models with localized feature extraction (e.g., CNN) are better suited to low-resource, structurally distinct scripts like Nüshu. Altogether, this study proposes CNN as a baseline and calls for hybrid models combining domain-specific embeddings and character-level features. More broadly, it highlights the role of NLP in preserving endangered scripts such as Nüshu.

## How to run:

### 1. Clone the repository: 
```bash
git clone https://github.com/alicellx6256/Nvshu-sentiment-analysis.git
cd Nvshu-sentiment-analysis
```
All dependencies are automatically installed in the notebook using !pip install. 

### 2. Launch the notebook
```bash
jupyter notebook
```

## My contribution: 
(My teammate and I experimented with four methods in total, so two each. To see my contribution, you only need to run Step 4 Method 1 and Method 3 in the jupyter notebook) 

- **Method 1: Fine-tuning bert-base-Chinese on Nushu sentences**: We fine-tuned BERT-base-
Chinese for sentence classification following the approach illustrated in Alammar’s visual tutorial. Sentences were encoded using BERT, and classification was performed using two methods: (1) a softmax classification layer applied to the [CLS] token embedding, as introduced by Devlin et al. (2019) and (2) a logistic regression classifier trained on frozen BERT embeddings, in line with the fine-tuning strategies explored by Sun et al. (2019) This method achieved the lowest performance with a macro average F1 score of 0.21 and a weighted average of 0.29. The model failed to identify any negative or neutral sentences (0 precision/recall for classes 0-1) and showed strong bias toward positive classification, correctly identifying all 57 positive sentences but achieving only 0.46 overall accuracy due to numerous false positives. This poor performance stems from class imbalance in the training set and, more critically, bert-base-Chinese's inability to properly tokenize Nüshu characters.
- **Method 3: Naïve Bayes classification**: Naïve Bayes: Using MultinomialNB from scikit-learn (Pedregosa et al., 2011), this model treated characters as independent features. It was computationally efficient but performed poorly (F1 = 0.42) due to the feature independence assumption and the sentences’ poetic, context-dependent nature. Our implementation follows early sentiment classification work by Pang, Lee, and Vaithyanathan (2002), who demonstrated the effectiveness of Naïve Bayes for text-based opinion mining. The Multinomial Naïve Bayes algorithm achieved a macro F1 score of 0.42 and a weighted average of 0.47, making it the second- best method with 52% accuracy on 100 samples (21 negative, 34 neutral, 45 positive). The model is strongly biased toward positive classification with high recall (0.87) but moderate precision (0.51), while achieving good precision but poor recall for negative sentences. The weak performance likely stems from the lack of a custom Nüshu tokenizer, as MNB relies heavily on meaningful character and word segmentation for effective bag-of-words and TF-IDF feature extraction.

## Reflections: 
- The importance of good and sufficient data: We obtained 500 Chinese-Nushu sentence pairs from a graduate student at Dartmouth who is conducting NLP research. The most significant barrier to accurate sentiment classification lies in our limited dataset of 500 sentences, which proved insufficient for robust pattern recognition across all tested models. Future research must prioritize substantial dataset expansion, coupled with a more rigorous manual annotation process that addresses the inherent emotional ambiguity characteristic of Chinese poetry. The development of standardized classification measures, including signal word identification and improved interrater reliability protocols, will be essential for creating consistent and accurate sentiment labels for training.
- The fundamental mismatch between Chinese (Mandarin) and Nushu characters, leading to improper tokenization: Our study highlights the fundamental mismatch between existing machine learning models trained on Mandarin Chinese and the unique linguistic properties of Xiangnan Tuhua represented through Nüshu characters. This disconnect necessitates the development of specialized natural language processing tools, including customized tokenizers specifically
designed for Nüshu's character system, to achieve meaningful sentiment analysis results. Next steps would be to train a custom Nushu tokenizer. 
