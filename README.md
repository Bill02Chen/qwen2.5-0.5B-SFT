# qwen2.5-0.5B-SFT
qwen2.5-0.5B SFT with OpenOrca dataset

1. Data cleaning strategy

The data cleaning strategy aims to solve includes formatting issues, quality issues, and consistency issues. For formatting issues, the strategy algorithm aims to address non-standard roles issues, and it will check missing fields issue and unmatched dialogue turns. For quality issues, the strategy algorithm checks empty and garbage text, character repetition text, template spam, and extremely short or long samples. For consistency issues, the strategy algorithm checks duplicated text and semantic consistency text.
Dataset is OpenOrca's first 1000K row data. With the above specific data cleaningstrategy, after data cleaning, there remain about 240K rows of data for fine tuning.

3. Training tuning

The base model is Qwen2.5-0.5B, the finetuning method is full finetuning. The key hyperparameter is listed here:
- Learning Rate: 1e-5
- Batch Size: 2
- Gradient Accumulation Step: 4
- Epochs: 2
- Warmup Steps: 0.1
- Learning Rate Scheduler: cosine
- Max Sequence Length: 1024
  
4. Evaluation results

The evaluation used MMLU (5-shot), ARC Easy (0-shot), ARC Challenge (25-shot),HellaSwag (10-shot), WinoGrande (5-shot), TruthfulQA (0-shot), PIQA (0-shot), and BoolQ (0-shot).
The evaluation scores for the 8 evaluation sets using the base model and the SFTmodel are shown in the following table.
Metric Base model SFT model
mmlu acc 0.2528±0.0037 0.4002±0.0041
arc-easy acc 0.4937±0.0103 0.5758±0.0101
acc-norm 0.4541±0.0102 0.4697±0.0102
arc-challenge acc 0.2918±0.0133 0.3123±0.0135
acc-norm 0.3336±0.0138 0.3439±0.0139
hellaswag acc 0.3838±0.0049 0.3855±0.0049
acc-norm 0.4949±0.0050 0.4814±0.0050
winogrande acc 0.5517±0.014 0.5612±0.0139
truthfulqa-mc2 acc 0.4262±0.0147 0.4309±0.0153
piqa acc 0.6893±0.0108 0.6823±0.0109
acc-norm 0.6872±0.0108 0.6774±0.0109
boolq acc 0.6321±0.0084 0.7177±0.0079
The table shows that after fine tuning, the accuracy scores in most evaluation sets areimproved. Particularly for MMLU and BoolQ evaluation sets, the accuracy scoresimprove significantly. The scores increase by about 58.3% and 13% respectively forthe MMLU and the BoolQ evaluation sets.

6. Conclusions & analysis

From the results, after fine tuning, there is a great improvement in MMLU and BoolQevaluation sets. Possibly due to the cleaned data in the small set of OpenOrca datasetis suitable for training knowledge and true or false type of questions.In conclusion, the finetuning successfully improves the performance of accuracy insome certain evaluation sets, especially MMLU, while preserving the performance ofthe base model in other evaluation sets.
