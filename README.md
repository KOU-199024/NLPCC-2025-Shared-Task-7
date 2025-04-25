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

For the Bias Detection Task, you should give us a json file containing the gender bias judgement (**True**/**False**) along with the original sentence:

```
{
    "text": "这思想开始火焰似的把她燃烧起来了，她再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。",
    "is_biased": true
}
```

### Subtask 2

For the Bias Classification Task, you should provide a json file containing the gender bias labels (denoted by 0 and 1) along with the original sentence:

```
{
    "ori_sentence": "这思想开始火焰似的把她燃烧起来了，她再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。",
    "bias_labels": [0, 1, 0]
}
```

### Subtask 3

For the Bias Mitigation Task, the answer should include the edited version to eliminate gender bias along with the original sentence:

```
{
    "ori_sentence": "这思想开始火焰似的把她燃烧起来了，她再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。",
    "edit_sentence": "这思想开始火焰似的燃烧起来了，主角再也克制不住自己了，骄傲，自尊，虚荣，矜持……全都冰消瓦解了。"
}
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
