# interpretable-language-fmri

This project investigates how well modern language models can predict and explain human brain activity during natural language processing, as measured by fMRI. Specifically, we develop voxel-level encoding models that map linguistic input to BOLD (Blood Oxygen Level Dependent) signals recorded from participants listening to naturalistic spoken narratives.

The project was completed as part of a three-part lab series from [UC Berkeley's STAT 214](https://graduate.catalog.berkeley.edu/courses/1654771) focused on neural encoding, embedding models, and interpretability. Across the three stages, we used off-the-shelf language embeddings, trained custom encoders, and fine-tuned transformer models, ultimately applying SHAP and LIME to interpret model behavior.

The [full final report](https://github.com/camccaffrey/interpretable-language-fmri/blob/main/reports/part-3.pdf) represents our group’s collective work. **My individual contributions to the report are isolated [here](https://github.com/camccaffrey/interpretable-language-fmri/blob/main/my-contributions/report.pdf)**, with all supporting materials and documentation in the `my-contributions` directory.


### Dataset

We use a curated subset of the [data](https://openneuro.org/datasets/ds002245) from [Jain & Huth (2018)](http://papers.neurips.cc/paper/7897-incorporating-context-into-language-encoding-models-for-fmri.pdf), which contains fMRI recordings from subjects listening to spoken narratives. For this project, we analyze BOLD (Blood Oxygen Level Dependent) signals from **two subjects** who each listened to **101 stories**. We used 75 stories for training and validation, reserving the remaining 26 for final model evaluation.

Each story is represented as a sequence of words (no punctuation or casing), aligned in time with the fMRI recordings. For each subject, the brain response to a story is stored as a 2D array of shape **T × V**, where:  
- **T** is the number of timepoints (TRs, or Time of Repetition units), which varies depending on the story's length.  
- **V** is the number of voxels recorded: **94,251 for Subject 2** and **95,556 for Subject 3**.

These voxel-level time series capture neural activity during naturalistic language processing and form the targets for our predictive models. Given the size and complexity of the voxel-wise fMRI data, we ran all models and analyses on the [Bridges-2 supercomputing cluster](https://www.psc.edu/resources/bridges-2/) using GPU resources provided through an [NSF ACCESS allocation](https://access-ci.org/). This enabled efficient training and evaluation of models at scale.




### Project Parts

##### [Part 1: Pre-trained Embeddings](https://github.com/camccaffrey/interpretable-language-fmri/blob/main/reports/part-1.pdf) 
We used off-the-shelf word embedding methods—Bag-of-Words, Word2Vec, and GloVe—to generate vector representations of words in naturalistic stories. These embeddings were aligned with fMRI data and used as input to ridge regression models to predict voxel-level BOLD responses.

##### [Part 2: Custom Encoder Training](https://github.com/camccaffrey/interpretable-language-fmri/blob/main/reports/part-2.pdf)  
We pre-trained a transformer-based encoder using a masked language modeling objective on the story transcripts. This provided contextualized embeddings tailored to the narrative data. These embeddings were then evaluated against those from Part 1 using the same ridge regression framework.

##### [Part 3: Fine-tuning and Interpretability](https://github.com/camccaffrey/interpretable-language-fmri/blob/main/reports/part-3.pdf)
We fine-tuned a pre-trained BERT model on the fMRI prediction task and explored parameter-efficient fine-tuning via LoRA. We then applied SHAP and LIME to interpret which words contributed most to the predictions for voxels with high model performance. This analysis aimed to link linguistic features to neural signals in an interpretable way.



### Contributors

- [Original Group Repository](https://github.com/xsgxlz/stat-214-lab3-group6) – Shared codebase and submissions from all team members.
- [Course Materials & Requirements](https://github.com/zachrewolinski/stat-214-gsi/tree/main/lab3/instructions) – Lab instructions and background provided by the course instructors.



