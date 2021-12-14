# [RE]Beyond Categorical Label Representations for Image Classification

### Original Authors
[Boyuan Chen](http://boyuanchen.com/),
[Yu Li](https://www.linkedin.com/in/lilykat),
[Sunand Raghupathi](https://www.linkedin.com/in/sunand-raghupathi),
[Hod Lipson](https://www.hodlipson.com/)
<br>
### Update on code as of 13/21/2021
[Imane Chafi]
[Marie Guertin]
[Arian Omidi]

## How to run the languages updated works (French, Russian, Canadian-French) 
1. Open```run.ipynb``` on a jupyter notebook
2. For the french translated labels, run ```!python train.py --model resnet110 --dataset cifar10 --label_dir ./labels/label_files/french --base_dir ./outputs/french --seed 7 --label speech``` under the Running tab
3. For the Russian accent labels, run ``` !python train.py --model resnet110 --dataset cifar10 --label_dir ./labels/label_files/russian --base_dir ./outputs/russian --seed 7 --label speech```
4. For the Canadian-french accent labels, run ```!python train.py --model resnet110 --dataset cifar10 --label_dir ./labels/label_files/chantel --base_dir ./outputs/chantel --seed 7 --label speech```
5. The results will be printed in the console

## How to run the limited dataset tests
1. Open```running_with_less_data.ipynb``` on a jupyter or google colab notebook
2. Sections titled VGG19 and RESNET110 with subtitles corresponding to 1%, 2%, 4%, 8%, 10% can be run in a notebook. 

## How to run the VGG19 and RESNET for plotting
1. Open```VGG19_RESNET110run.ipynb``` on a jupyter or google colab notebook
2. To run VGG19 or RESNET110, simply change the ```--model``` tag to ```--model resnet110``` or ```--model VGG19``` from the above instructions
3. To output the graphs, run the last section titled ```Graphs```

### For more running information, and to run the original code paper, please see below. 

bbbb
Columbia University
<br>
[International Conference on Learning Representations (ICLR 2021)](https://openreview.net/forum?id=MyHwDabUHZm)

### [Project Website](https://www.creativemachineslab.com/label-representation.html) | [Video](https://www.youtube.com/watch?v=Iq2YjHCAPRQ&t) | [Paper](https://openreview.net/forum?id=MyHwDabUHZm) | [Arxiv](https://arxiv.org/abs/2104.02226)

## Overview
This repo contains the PyTorch implementation for paper "Beyond Categorical Label Representations for Image Classification".
[![teaser](figures/teaser.png)](https://www.youtube.com/watch?v=Iq2YjHCAPRQ&t)

## Content

- [Installation](#installation)
- [Data Preparation](#data-preparation)
- [About the labels](#about-the-labels)
- [Training](#training)
- [Attacks](#attacks)
- [Training with Less Data](#training-with-less-data)
- [Shared Utilities](#shared-utilities)

## Installation

Create a python virtual environment and install the dependencies.

```bash
virtualenv -p /usr/bin/python3.6 env3.6
source env3.6/bin/activate
pip install -r requirements.txt
```

## Data Preparation

Download the CIFAR10 and CIFAR100 datasets by running:
```bash
mkdir ./data
cd ./data
wget https://www.cs.toronto.edu/\~kriz/cifar-10-python.tar.gz
wget https://www.cs.toronto.edu/\~kriz/cifar-100-python.tar.gz
cd ..
```

## About the labels
All labels are pre-generated in the labels folders and ready to be loaded directly for training. The notebook **labels/labels.ipynb** contains code for generating these labels.

Label types (```--label```):
- Category: **category**
- High-dimensional: **speech**, **uniform**, **shuffle**, **composite**, **bert**, and **random**
- Low-dimensional: **lowdim** and **glove**

Base model types (```--model```): **vgg19**, **resnet32**, and **resnet110**

Datasets (```--dataset```): **cifar10** and **cifar100** for cifar10 and cifar100

Seed (```--seed```): an int value for seeding data loading sequence

Data Level (```--level```): an int percentage (<90) for training with level% of all data (defaults to 100)

Base directory (```--base_dir```): location to save training/attacking results (required)

Label directory (```--label_dir```): location where label files are located (defaults to ```./labels/label_files```)

The **labels/label_files** folder contains the labels stored in .npy files.

* cifar10 high-dim labels:
* shape (10, 64, 64)
* dtype float32

* cifar100 high-dim labels:
* shape (100, 64, 64)
* dtype float32

You can find the original audio used to generate the speech labels in **labels/cifar10_wav/** and **labels/cifar100_wav/**. You can view the grayscale images of all composite labels (rescaled to 0-255) in **labels/composite/**.

## Training

Now to train the models use the following.
- Category: use **train.py** and specify label ```--label category```
```bash
python3 train.py --model resnet110 --dataset cifar10 --seed 7 --label category
```

- High-dimensional: use **train.py** and specify a particular high-dimensional label
```bash
python3 train.py --model vgg19 --dataset cifar100 --seed 77 --label speech
```
## Attacks
Run both targeted and untargeted FGSM and iterative attacks against trained models.
- Category: use **attack.py**
```bash
python3 attack.py --model resnet110 --dataset cifar10 --seed 7 --label category
```
- High-dimensional: use **attack.py** and specify a particular high-dimensional label
```bash
python3 attack.py --label speech --model vgg19 --dataset cifar100 --seed 77
```

## Training with Less Data
Use the same training files as before, but specify a data level.

- Category: use **train.py** to train with 2% data
```bash
python3 train.py --model resnet110 --dataset cifar10 --seed 7 --label category --level 2
```

- High-dimensional: use **train.py** to train with 8% data
```bash
python3 train.py --model vgg19 --dataset cifar100 --seed 77 --label speech --level 8
```

## Shared Utilities
- **architecture.py**: where the category and high-dimensional models are defined
- **cifar.py**: for loading cifar10 and cifar100 dataset for all label types
- **utils/trainutil.py**: other training helpers

## BibTex

```
@inproceedings{chen2021beyond,
  title={Beyond Categorical Label Representations for Image Classification},
  author={Chen, Boyuan and Li, Yu and Raghupathi, Sunand and Lipson, Hod},
  booktitle={The International Conference on Learning Representations},
  year={2021}
}
```

## License

This repository is released under the MIT license. See [LICENSE](LICENSE) for additional details.
