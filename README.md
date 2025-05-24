# NLPCC-2025-Shared-Task-7

Chinese Gender Bias Probing and Mitigation Task

# Task Introduction

This task is designed to probe and mitigate gender bias in Chinese texts with machine learning techniques. It is divided into three subtasks:

SUBTASK 1. Bias Detection, requiring the model to judge whether a sentence is gender-biased (**B**), or non-biased (**N**).

SUBTASK 2. Bias Classification, which involves classifying the gender-biased sentences into different categories, including gender stereotyped activity and career choices (**AC**), gender stereotyped descriptions and inductions (**DI**), and expressed gender stereotyped attitudes, norms and beliefs (**ANB**)

SUBTASK 3. Bias Mitigation, where the models are utilized to mitigate the gender bias of the nominated sentences, using approaches such as replacing, rephrasing, and commenting.

## Data Description & Rules

### Train & Validation Data

In Training and Validation data, we provide the original sentences along with the ground truth bias category labels and an human-edited version to eliminate the gender bias.

#### Biased Data

In our biased data we provide the format like:

```
{
    'ori_sentence': '这思想开始火焰似的把她燃烧起来了，她再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。',
    'bias_labels': [0, 1, 0],
    'edit_sentence':  '这思想开始火焰似的燃烧起来了，主角再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。'
}
```

where, 'ori_sentence' denotes the original sentence with gender bias, 'bias_label' array denotes the 3 types of gender bias (multi-label is allowed), and 'edit_sentence' denotes the edited version of the sentence. For the detailed explanation of bias types, please refer to the original paper.

**we allow you to use extra data apart from our provided training data**

#### Non-Biased Data:

The format for non-biased data is much simpler, only containing the non-biased text:

```
{
    "text": "然而凭着顽强的毅力,她努力学习按摩技术,通过自学取得了大专文凭,成为嘉兴唯一一名盲人中医师。"
}
```

**we allow you to use extra data apart from our provided training data**

### Test Data

#### Subtask 1 (Detection)

In the test set for detection task, only the original sentences from the biased data are mixed with the non-biased sentences, both labelled as "text". Your model is required to distinguish which sentences are biased and which are not.

```
 {
     "text": "她讲起话来，总是尖声尖气，扭扭捏捏。"
 }
```

#### Subtask 2/3 (Classfication and Mitigation)

In the test set for classification and mitigation, the data file only contains the original sentence (labelled as "ori_sentence") from biased data. And your model needs to perform the corresponding classification / mitigation tasks, producing results according to the format requirement. Please refer to the **Submission** section.

```
{
    "ori_sentence": "这思想开始火焰似的把她燃烧起来了，她再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。"
}
```

## Submission

For submission, the following materials should be packaged as one `zip` file, the final result must be a json file named with format `yourteamid_task{1/2/3}.json` and sent to [yizhi.li@hotmail.com](mailto:yizhi.li@hotmail.com) or [hanhua.hong@postgrad.manchester.ac.uk](mailto:hanhua.hong@postgrad.manchester.ac.uk):

### Subtask 1

For the Bias Detection Task, you should give us a single json file containing the gender bias judgement (**True**/**False**) along with the original sentences:

```
[
    {
        "text": "这思想开始火焰似的把她燃烧起来了，她再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。",
        "is_biased": true
    },
    ...
]
```

### Subtask 2

For the Bias Classification Task, you should provide a single json file containing the gender bias labels (denoted by 0 and 1) along with the original sentences:

```
[
    {
        "ori_sentence": "这思想开始火焰似的把她燃烧起来了，她再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。",
        "bias_labels": [0, 1, 0]
    },
    ...
]
```

### Subtask 3

For the Bias Mitigation Task, the answer should include the edited version to eliminate gender bias along with the original sentences:

```
[
    {
        "ori_sentence": "这思想开始火焰似的把她燃烧起来了，她再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。",
        "edit_sentence": "这思想开始火焰似的燃烧起来了，主角再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。"
    },
    ...
]
```

## Evaluation

The top 3 participating teams in each task and track will be certificated by NLPCC and CCF-NLP.

## Contact & Citation

If your publication employs our dataset, please cite the following article:

```\
@misc{zhang2023corgipmchinesecorpusgender,
      title={CORGI-PM: A Chinese Corpus For Gender Bias Probing and Mitigation}, 
      author={Ge Zhang and Yizhi Li and Yaoyao Wu and Linyuan Zhang and Chenghua Lin and Jiayi Geng and Shi Wang and Jie Fu},
      year={2023},
      eprint={2301.00395},
      archivePrefix={arXiv},
      primaryClass={cs.CL},
      url={https://arxiv.org/abs/2301.00395}, 
}
```

If you have any questions about this task, please email to [yizhi.li@hotmail.com](mailto:yizhi.li@hotmail.com) or [hanhua.hong@postgrad.manchester.ac.uk](mailto:hanhua.hong@postgrad.manchester.ac.uk).

# Ranking

Our baseline model for the evaluation is [MAP-Neo](https://map-neo.github.io/), which is marked in italics in the table

## Subtask 1: Detection Task

| Ranking | Team Name     | Precision | Recall | F1    |
| ------- | ------------- | --------- | ------ | ----- |
| 1       | ZZU-nlp       | 0.798     | 0.910  | 0.850 |
| 2       | ZZU-NLP_DS    | 0.604     | 0.960  | 0.741 |
| 3       | Cloud Lab     | 0.566     | 0.990  | 0.720 |
| 4       | YNU-HPCC      | 0.645     | 0.800  | 0.714 |
| 5       | Prompt        | 0.552     | 1.000  | 0.712 |
| 6       | IR901         | 0.557     | 0.980  | 0.710 |
| 7       | xlarge        | 0.536     | 0.960  | 0.688 |
| 8       | Hu            | 0.522     | 0.970  | 0.678 |
| 9       | wangkongqiang | 0.565     | 0.830  | 0.672 |
| 10      | *MAP-Neo*   | 0.495     | 0.960  | 0.653 |
| 11      | Team0071      | 0.496     | 0.640  | 0.559 |

## Subtask 2: Classification Task

| Ranking | Team Name     | Precision | Recall | F1    |
| ------- | ------------- | --------- | ------ | ----- |
| 1       | ZZU-nlp       | 0.543     | 0.576  | 0.646 |
| 2       | Team0071      | 0.511     | 0.591  | 0.548 |
| 3       | Hu            | 0.447     | 0.658  | 0.531 |
| 4       | *MAP-Neo*   | 0.436     | 0.677  | 0.526 |
| 5       | YNU-HPCC      | 0.463     | 0.565  | 0.509 |
| 6       | Prompt        | 0.496     | 0.513  | 0.505 |
| 7       | Tsingyi       | 0.479     | 0.468  | 0.474 |
| 8       | Cloud Lab     | 0.510     | 0.409  | 0.453 |
| 9       | IR901         | 0.443     | 0.420  | 0.431 |
| 10      | ZZUNLP_DS     | 0.466     | 0.361  | 0.407 |
| 11      | wangkongqiang | 0.484     | 0.283  | 0.357 |

## Subtask 3: Mitigation Task

| Ranking | Team Name   | BLEU  | METEOR | ROUGE-L_P | ROUGE-L_R | ROUGE-L_F1 | Average |
| ------- | ----------- | ----- | ------ | --------- | --------- | ---------- | ------- |
| 1       | ZZU-nlp     | 0.013 | 0.417  | 0.464     | 0.452     | 0.452      | 0.294   |
| 2       | Team0071    | 0.013 | 0.419  | 0.466     | 0.450     | 0.448      | 0.293   |
| 3       | YNU-HPCC    | 0.013 | 0.414  | 0.472     | 0.448     | 0.453      | 0.293   |
| 4       | Prompt      | 0.011 | 0.418  | 0.430     | 0.462     | 0.434      | 0.288   |
| 5       | IR901       | 0.010 | 0.399  | 0.385     | 0.454     | 0.403      | 0.271   |
| 6       | ZZUNLP_DS   | 0.010 | 0.393  | 0.372     | 0.458     | 0.397      | 0.267   |
| 7       | Cloud Lab   | 0.009 | 0.391  | 0.367     | 0.461     | 0.394      | 0.265   |
| 8       | Hu          | 0.005 | 0.106  | 0.158     | 0.237     | 0.187      | 0.099   |
| 9       | *MAP-Neo* | 0.009 | 0.108  | 0.213     | 0.130     | 0.155      | 0.091   |

## Overall Result

| Ranking | Team Name   | Subtask1 | Subtask2 | Subtask3 | Average |
| ------- | ----------- | -------- | -------- | -------- | ------- |
| 1       | ZZU-nlp     | 0.850    | 0.646    | 0.294    | 0.597   |
| 2       | YNU-HPCC    | 0.714    | 0.509    | 0.293    | 0.505   |
| 3       | Prompt      | 0.712    | 0.505    | 0.288    | 0.502   |
| 4       | Cloud Lab   | 0.720    | 0.453    | 0.265    | 0.479   |
| 5       | ZZUNLP_DS   | 0.741    | 0.407    | 0.267    | 0.472   |
| 6       | IR901       | 0.710    | 0.431    | 0.271    | 0.471   |
| 7       | Team0071    | 0.559    | 0.548    | 0.293    | 0.467   |
| 8       | Hu          | 0.678    | 0.531    | 0.099    | 0.436   |
| 9       | *MAP-Neo* | 0.653    | 0.526    | 0.091    | 0.423   |
