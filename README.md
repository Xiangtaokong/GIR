# GIR
A Preliminary Exploration Towards General Image Restoration

[Paper]()|[DataSet]() 

Authors: Xiangtao Kong, [Jinjin GU](https://www.jasongt.com/), [Yihao Liu](https://scholar.google.com/citations?user=WRIYcNwAAAAJ&hl=en&oi=ao), [Wenlong Zhang](https://wenlongzhang0517.github.io/), [Xiangyu Chen](https://chxy95.github.io/), [Yu Qiao](https://scholar.google.com/citations?user=gFtI-8QAAAAJ&hl=zh-CN), [Chao Dong](https://scholar.google.com.hk/citations?user=OSDCB0UAAAAJ&hl=zh-CN)

![Demo Image]()

## Abstract

Despite the tremendous success of deep models in various individual image restoration tasks, at least two technical challenges prevent these works from being applied to real-world usages: (1) the lack of generalization ability and (2) complex and unknown degradations in real-world usages. These two challenges fail existing deep models developed only for individual image restoration tasks. In this paper, we present a new problem called general image restoration (GIR) which aims to address these challenges with a unified model. GIR covers most individual image restoration tasks (\eg, image denoising, deblurring, deraining and super-resolution) and their combinations for general purposes. We discuss the definition of GIR and present that the core characteristics of GIR are the generality and generalization performance. We also propose new datasets and discuss how to evaluate GIR models. After that, we benchmark existing possible approaches to GIR. By these approaches we show the superiority and practical difficult of GIR. At last, we also try to understand and interpret these model behaviours to inspire the future direction. Our work can open up new valuable research directions and contribute to the research of general vision.


## Dependencies

- Python >= 3.6 (Recommend to use [Anaconda](https://www.anaconda.com/download/#linux))
- [PyTorch >= 1.5.0](https://pytorch.org/)
- NVIDIA GPU + [CUDA](https://developer.nvidia.com/cuda-downloads)
- Python packages: `pip install numpy opencv-python`
- [option] Python packages: [`pip install tensorboardX`](https://github.com/lanpa/tensorboardX), for visualizing curves.

# Codes 
- Our codes version based on [BasicSR](https://github.com/xinntao/BasicSR). 

## How to evaluate a GIR model
1. Clone this github repo. 
```
git clone https://github.com/Xiangtaokong/ClassSR.git
cd ClassSR
```
2. Download the testing datasets ([DIV2K_valid](https://data.vision.ee.ethz.ch/cvl/DIV2K/)). 

3. Download the [divide_val.log](https://drive.google.com/file/d/1zMDD9Z_-fM2R2qm2QLoq7N2LMG6V92JT/view?usp=sharing) and move it to `.codes/data_scripts/`.

4. Generate simple, medium, hard (class1, class2, class3) validation data. 
```
cd codes/data_scripts
python extract_subimages_test.py
python divide_subimages_test.py
```
5. Download [pretrained models](https://drive.google.com/drive/folders/1jzAFazbaGxHb-xL4vmxc-hHbR1J-uek_?usp=sharing) and move them to  `./experiments/pretrained_models/` folder. 

6. Run testing for a single branch.
```
cd codes
python test.py -opt options/test/test_FSRCNN.yml
python test.py -opt options/test/test_CARN.yml
python test.py -opt options/test/test_SRResNet.yml
python test.py -opt options/test/test_RCAN.yml
```

7. The output results will be sorted in `./results`. 

## How to generate various degraded images
1. Clone this github repo. 
```
git clone https://github.com/Xiangtaokong/ClassSR.git
cd ClassSR
```

2. Download the testing datasets (Test2K, 4K, 8K) [Google Drive](https://drive.google.com/drive/folders/18b3QKaDJdrd9y0KwtrWU2Vp9nHxvfTZH?usp=sharing) or [Baidu Drive](https://pan.baidu.com/s/1OARDfd2x3ynQs7m1tu_RnA) (Password: 7dw1) .

3. You can also download the source data [DIV8K](https://competitions.codalab.org/competitions/22217#participate). Test8K contains the images (index 1401-1500) from DIV8K. Test2K/4K contain the images (index 1201-1300/1301-1400) from DIV8K which are downsampled to 2K and 4K resolution. (In this way, you need register for the competition (Ntire 2020 was held on 2020, but we can register now), then you can download DIV8K dataset.)

4. Download [pretrained models](https://drive.google.com/drive/folders/1jzAFazbaGxHb-xL4vmxc-hHbR1J-uek_?usp=sharing) and move them to  `./experiments/pretrained_models/` folder. 

5. Run testing for ClassSR.
```
cd codes
python test_ClassSR.py -opt options/test/test_ClassSR_FSRCNN.yml
python test_ClassSR.py -opt options/test/test_ClassSR_CARN.yml
python test_ClassSR.py -opt options/test/test_ClassSR_SRResNet.yml
python test_ClassSR.py -opt options/test/test_ClassSR_RCAN.yml
```
6. The output results will be sorted in `./results`. 


## How to train existing potential methods in paper
1. Clone this github repo. 
```
git clone https://github.com/Xiangtaokong/ClassSR.git
cd ClassSR
```
2. Download the training datasets([DIV2K](https://data.vision.ee.ethz.ch/cvl/DIV2K/)) and validation dataset(Set5).

3. Download the [divide_train.log](https://drive.google.com/file/d/1WhyYYZHfpoNEjslojuqZLR46Nlr15zqQ/view?usp=sharing) and move it to `.codes/data_scripts/`.

4. Generate simple, medium, hard (class1, class2, class3) training data. 
```
cd codes/data_scripts
python data_augmentation.py
python generate_mod_LR_bic.py
python extract_subimages_train.py
python divide_subimages_train.py
```

5. Run training for a single branch (default branch1, the simplest branch).
```
cd codes
python train.py -opt options/train/train_FSRCNN.yml
python train.py -opt options/train/train_CARN.yml
python train.py -opt options/train/train_SRResNet.yml
python train.py -opt options/train/train_RCAN.yml
```
6. The experiments will be sorted in `./experiments`. 

## How to use the interpretation methods

1. Clone this github repo. 
```
git clone https://github.com/Xiangtaokong/ClassSR.git
cd ClassSR
```
2. Download the training datasets ([DIV2K](https://data.vision.ee.ethz.ch/cvl/DIV2K/)) and validation dataset([DIV2K_valid](https://data.vision.ee.ethz.ch/cvl/DIV2K/), index 801-810). 


3. Generate training data (the all data(1.59M) in paper).
```
cd codes/data_scripts
python data_augmentation.py
python generate_mod_LR_bic.py
python extract_subimages_train.py
```
4. Download [pretrained models](https://drive.google.com/drive/folders/1jzAFazbaGxHb-xL4vmxc-hHbR1J-uek_?usp=sharing)(pretrained branches) and move them to  `./experiments/pretrained_models/` folder. 

5. Run training for ClassSR.
```
cd codes
python train_ClassSR.py -opt options/train/train_ClassSR_FSRCNN.yml
python train_ClassSR.py -opt options/train/train_ClassSR_CARN.yml
python train_ClassSR.py -opt options/train/train_ClassSR_SRResNet.yml
python train_ClassSR.py -opt options/train/train_ClassSR_RCAN.yml
```
6. The experiments will be sorted in `./experiments`. 

## How to generate demo images

Generate demo images like this one:

![Demo Image](https://raw.githubusercontent.com/Xiangtaokong/ClassSR/main/demo_images/show.png)

Change the 'add_mask: False' to True in test_ClassSR_xxx.yml and run testing for ClassSR.

## Citation
```
@InProceedings{Kong_2021_CVPR,
    author    = {Kong, Xiangtao and Zhao, Hengyuan and Qiao, Yu and Dong, Chao},
    title     = {ClassSR: A General Framework to Accelerate Super-Resolution Networks by Data Characteristic},
    booktitle = {Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition (CVPR)},
    month     = {June},
    year      = {2021},
    pages     = {12016-12025}
}
```

## Contact
Email: xt.kong@siat.ac.cn

