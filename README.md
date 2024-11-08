# LabelAId: AI Interventions for Improving Human Labeling Quality and Domain Knowledge in Crowdsourcing Systems
LabelAId is an advanced inference model combining Programmatic Weak Supervision (PWS) with Feature Tokenizer + Transformer (FT-Transformer) to infer label correctness based on user behavior and domain knowledge. Check out our [paper](https://dl.acm.org/doi/pdf/10.1145/3613904.3642089) and [video](https://youtu.be/53Cmxsqjphg) for more details.

![LabelAId](/figures/labelaid-teaser.png)

This repository contains the data, model code, evaluation code for *LabelAId: AI Interventions for Improving Human Labeling Quality and Domain Knowledge in Crowdsourcing Systems* by Chu Li*, Zhihan Zhang*, Michael Saugstad, Esteban Safranchik, Minchu Kulkarni, Xiaoyu Huang, Shwetak Patel, Vikram Iyer, Tim Althoff, Jon E. Froehlich. The paper was published in Proceedings of the CHI Conference on Human Factors in Computing Systems (CHI’24).

## LabelAId Pipeline
The LabelAId machine learning pipeline consists of two phases, programmatic weak supervision for annotating raw data, and discriminative machine learning models for downstream tasks.

![Pipeline](/figures/labelaid-LF-pipeline.png "This is the image caption")


To study LabelAId in a real world context, we instrumented the open-source crowdsourcing tool, Project Sidewalk. When integrating LabelAId with Project Sidewalk, we chose the FT-transformer model as the discriminative model, as it is designed to handle tabular data with mixed numerical and categorical features, therefore it aligns with the heterogeneous nature of the Project Sidewalk dataset.

![FT-Transformer](/figures/labelaid-transformer-diagram.png "This is the image caption")


See our code for [PWS](/model-pipeline/PWS.ipynb) and [FT-Transformer](/model-pipeline/FT-Transformer.ipynb) for more details.

## Datasets
Our [datasets](/datasets) come from Project Sidewalk labels from Seattle, WA; Chicago, IL; and Oradell, NJ. The unannotated set is used to pre-train the model after our PWS annotation process. The expert-validated set is used to fine-tune and evaluate the inference model, which was created from labels manually-validated by the Project Sidewalk research team.

| Label Type            | Seattle Unannotated | Seattle Expert-Validated | Chicago Unannotated | Chicago Expert-Validated | Oradell Unannotated | Oradell Expert-Validated | Total   |
|-----------------------|----------------------|---------------------------|----------------------|--------------------------|---------------------|--------------------------|---------|
| Curb Ramp             | 70,690              | 5,333                     | 5,710                | 2,386                    | 660                 | 859                      | 85,638  |
| Missing Curb Ramp     | 32,968              | 4,239                     | 463                  | 1,294                    | 325                 | 396                      | 39,685  |
| No Sidewalk           | 36,021              | 3,460                     | 2,211                | 48                       | 3,949               | 1,217                    | 46,906  |
| Surface Problem       | 26,912              | 2,909                     | 2,136                | 1,651                    | 2,544               | 1,222                    | 37,374  |
| Obstacle              | 10,103              | 407                       | 1,254                | 320                      | 106                 | 158                      | 12,348  |
| **All Label Types**   | **176,694**         | **16,348**                | **11,774**           | **5,699**                | **7,584**           | **3,852**                | **221,951** |

## Technical Evaluation
LabelAId consistently outperforms all other baseline models and can improve mistake inference accuracy by up to 37% with just 50 downstream samples. See our [evaluation code](/evaluation/evaluation.ipynb) and paper for more details.

![Techinical Evaluation](/figures/labelaid-accuracy-f1.png "This is the image caption")


## User Study
Having demonstrated the technical efficacy of our LabelAId system in inferring label correctness, we implemented the LabelAId inference model in Project Sidewalk, and evaluated the user experience and performance of the end-to-end system with users in the loop.

![User flow](/figures/labelaid-user-flow.png "A user flow diagram of LabelAId implemented in Project Sidewalk.")

The code for integrating LabelAId pipeline with Project Sidewalk labeling interface can be found [here](https://github.com/ProjectSidewalk/SidewalkWebpage/blob/62d300018634b6c22172f7168779e61a5f643a25/public/javascripts/SVLabel/src/SVLabel/PredictionModel.js#L662).

### Cite LabelAId
```
@inproceedings{10.1145/3613904.3642089,
author = {Li, Chu and Zhang, Zhihan and Saugstad, Michael and Safranchik, Esteban and Kulkarni, Chaitanyashareef and Huang, Xiaoyu and Patel, Shwetak and Iyer, Vikram and Althoff, Tim and Froehlich, Jon E.},
title = {LabelAId: Just-in-time AI Interventions for Improving Human Labeling Quality and Domain Knowledge in Crowdsourcing Systems},
year = {2024},
isbn = {9798400703300},
publisher = {Association for Computing Machinery},
address = {New York, NY, USA},
url = {https://doi.org/10.1145/3613904.3642089},
doi = {10.1145/3613904.3642089},
booktitle = {Proceedings of the 2024 CHI Conference on Human Factors in Computing Systems},
articleno = {643},
numpages = {21},
keywords = {community science, crowdsourcing, human-ai collaboration, machine learning, programmatic weak supervision (pws), quality control, urban accessibility},
location = {Honolulu, HI, USA},
series = {CHI '24}
}
```