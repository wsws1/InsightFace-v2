# InsightFace

![apm](https://img.shields.io/apm/l/vim-mode.svg)

PyTorch implementation of Additive Angular Margin Loss for Deep Face Recognition.
[paper](https://arxiv.org/pdf/1801.07698.pdf).
```
@article{deng2018arcface,
title={ArcFace: Additive Angular Margin Loss for Deep Face Recognition},
author={Deng, Jiankang and Guo, Jia and Niannan, Xue and Zafeiriou, Stefanos},
journal={arXiv:1801.07698},
year={2018}
}
```
## DataSet

MS-Celeb-1M DataSet, 3,804,846 faces over 85,164 identities.

## Dependencies
- PyTorch 1.0.0

## Usage

### Data wrangling
Extract images, scan them, to get bounding boxes and landmarks:
```bash
$ python pre_process.py
```

Image alignment:
1. Face detection(MTCNN).
2. Face alignment(similar transformation).
3. Central face selection.
4. Resize -> 112x112. 

Original | Aligned | Original | Aligned |
|---|---|---|---|
|![image](https://github.com/foamliu/InsightFace/raw/master/images/0_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/0_img.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/1_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/1_img.jpg)|
|![image](https://github.com/foamliu/InsightFace/raw/master/images/2_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/2_img.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/3_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/3_img.jpg)|
|![image](https://github.com/foamliu/InsightFace/raw/master/images/4_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/4_img.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/5_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/5_img.jpg)|
|![image](https://github.com/foamliu/InsightFace/raw/master/images/6_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/6_img.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/7_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/7_img.jpg)|
|![image](https://github.com/foamliu/InsightFace/raw/master/images/8_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/8_img.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/9_raw.jpg)|![image](https://github.com/foamliu/InsightFace/raw/master/images/9_img.jpg)|

### Train
```bash
$ python train.py
```

To visualize the training process：
```bash
$ tensorboard --logdir=runs
```

## Performance evaluation

### DataSet
Use Labeled Faces in the Wild (LFW) dataset for performance evaluation:

- 13233 faces
- 5749 identities
- 1680 identities with >=2 photo

Download LFW database put it under data folder:
```bash
$ wget http://vis-www.cs.umass.edu/lfw/lfw-funneled.tgz
$ wget http://vis-www.cs.umass.edu/lfw/pairs.txt
$ wget http://vis-www.cs.umass.edu/lfw/people.txt
```

### Get it started

```bash
$ python lfw_eval.py
```

### Results
Backbones|LFW(%)|Download|
|---|---|---|
|SE-LResNet101E-IR|99.75%|[Link]()|
|SE-LResNet18E-IR|99.58%|[Link](https://github.com/foamliu/InsightFace-v2/releases/download/v1.0/BEST_checkpoint_r18.tar)|

### theta j Distribution

![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/theta_dist.png)

### Error analysis
##### False Positive
0 false positives:

##### False Negative
15 false negative, these 10 are randomly chosen:

1|2|1|2|
|---|---|---|---|
|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/0_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/0_fn_1.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/1_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/1_fn_1.jpg)|
|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/2_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/2_fn_1.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/3_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/3_fn_1.jpg)|
|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/4_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/4_fn_1.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/5_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/5_fn_1.jpg)|
|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/6_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/6_fn_1.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/7_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/7_fn_1.jpg)|
|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/8_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/8_fn_1.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/9_fn_0.jpg)|![image](https://github.com/foamliu/InsightFace-v2/raw/master/images/9_fn_1.jpg)|
 