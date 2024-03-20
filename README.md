# PRO-GENE-GEN
[![LICENSE](https://img.shields.io/badge/license-MIT-green?style=flat-square)](LICENSE)
[![Python](https://img.shields.io/badge/python-3.9-blue.svg?style=flat-square)](https://www.python.org/)
[![PyTorch](https://img.shields.io/badge/PyTorch-2.2.0-orange)](https://pytorch.org/)

![image](teaser_figure.jpg)
*On the left side, we illustrate the performance of various privacy models based on a standard Machine Learning Efficacy metric. This evaluation assesses the utility of each model in downstream machine learning tasks. Conversely, on the right side, we evaluate the models using a biological metric known as DE-Gene Preservation. This specific metric examines whether models can maintain the co-expression patterns observed in the actual data, with a focus on Pearson correlation values greater than 0.The **X-axis** across both evaluations represents a range of privacy budgets, spanning from relatively low to high. This axis allows us to compare the impact of different privacy levels on model performance. Additionally, **Real data (reference)** is depicted, which pertains to the metrics obtained directly from the real data (comparison of training versus test datasets). This serves as a benchmark or oracle score, indicating the optimal performance that models aim to achieve.*


This repository contains the implementation for ["Towards Biologically Plausible and Private Gene Expression Data Generation" (PoPETs 2024)](https://arxiv.org/pdf/2402.04912.pdf).

*Authors: \*Dingfan Chen, \*Marie Oestreich, \*Tejumade Afonja, Raouf Kerkouche, Matthias Becker, and Mario Fritz* (\*: equal authorship)

Contact: Dingfan Chen ([dingfan.chen@cispa.de](mailto:dingfan.chen@cispa.de)), Marie Oestreich ([Marie.Oestreich@dzne.de](mailto:marie.oestreich@dzne.de)), or Tejumade Afonja ([tejumade.afonja@cispa.de](mailto:tejumade.afonja@cispa.de))



## Requirements
This implementation is based on [PyTorch](https://pytorch.org/) (tested for version 2.2.0). Please refer to [requirements.txt](./requirements.txt) for the other required packages and version.  

## Setup
- Create a virtual environment

        python -m venv .venv

- Activate the virtual environment
    
        source .venv/bin/activate

- Install the required packages

        pip install -r requirements.txt


## Dataset
The generative models were trained on a bulk RNA-seq dataset compiled by Warnat-Herresthal[1]. Each row represents a biological specimen obtained from a patient, while each column indicates the expression level of a particular gene. The expression levels are quantified by RNA-seq counts, with higher integer values indicating greater gene activity. It comprises samples from 5 disease classes, 4 classes of which are types of leukemia and the fifth class is the category 'Other', which is made up of samples from various other diseases as well as healthy controls. The 4 leukemia types are acute myeloid leukemia (AML), acute lymphocytic leukemia (ALL), chronic myeloid leukemia (CML) and chronic lymphocytic leukemia (CLL).

You can be download the dataset [here](https://dl.cispa.de/s/X2AnxmLrmGtQk7X). We have also prepared a notebook to inspect the dataset and preprocess.

    data/aml/data-inspect.ipynb

## Running Experiments
We investigated 5 representative generative models [VAE](./models/VAE), [GAN](./models/DP_WGAN), [Private-PGM](./models/Private_PGM), [PrivSyn](./models/DPSYN), and [Ron-Gauss](./models/RONgauss).

### API
Change to the model directory e.g [vae](./models/VAE)  

        cd models/VAE

You can train the model by running the bash script;

        bash loop.sh

For vae model, we provide script to run the membership inference attack;

        bash loop_mia.sh

### Evaluation
The biological and statistical evaluation script for the synthetic data can be found in [eval](./eval/) folder. We attached a README which instruct on how to download the `eval_data` used to generate the figures in the paper.

## Citation
```bibtex
@article{chen2024towards,
  title={Towards Biologically Plausible and Private Gene Expression Data Generation},
  author={Chen, Dingfan and Oestreich, Marie and Afonja, Tejumade and Kerkouche, Raouf and Becker, Matthias and Fritz, Mario},
  journal={Proceedings on Privacy Enhancing Technologies},
  year={2024}
}
```

## Acknowledgements
Our implementation uses the source code from the following repositories:
- [Private Data Generation](https://github.com/BorealisAI/private-data-generation)

- [DPSyn](https://github.com/usnistgov/PrivacyEngCollabSpace/tree/master/tools/de-identification/Differential-Privacy-Synthetic-Data-Challenge-Algorithms/DPSyn)

- [hCoCena](https://github.com/MarieOestreich/hCoCena)

- [MargCTGAN](https://github.com/tejuafonja/margctgan)

## References
[1] Warnat-Herresthal, S., Perrakis, K., Taschler, B., Becker, M., Baßler, K., Beyer, M., Günther, P., Schulte-Schrepping, J., Seep, L., Klee, K. and Ulas, T., 2020. Scalable prediction of acute myeloid leukemia using high-dimensional machine learning and blood transcriptomics. Iscience, 23(1).
