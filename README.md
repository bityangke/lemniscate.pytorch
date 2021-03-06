## Unsupervised Feature Learning via Non-parameteric Instance Discrimination

This repo constains the pytorch implementation for the CVPR2018 unsupervised learning paper.

```
@inproceedings{unsupervised2018wu,
  title={Unsupervised Feature Learning via Non-parametric Instance-level Discrimination},
  author={Wu, Zhirong and Xiong, Yuanjun and Yu, Stella and Lin, Dahua},
  booktitle={Computer Vision and Pattern Recognition (CVPR) 2018},
  year={2018}
}
```

## Highlight

- We formulate unsupervised learning from a completely different non-parametric perspective.
- Feature encodings can be as compact as 128 dimension for each image.
- Enjoys the benefit of advanced architectures and techniques from supervised learning.
- Runs seamlessly with nearest neighbor classifiers.

## Pretrained Model

Currently, we provides pretrained models of ResNet 18 and ResNet 50. Each tar ball contains the feature representation of all ImageNet training images (600 mb) and model weights (100-200mb).

- [ResNet 18]() (top 1 accuracy 41.0% )
- [ResNet 50]() (top 1 accuracy 46.8%)

## Usage

Our code extends the pytorch implementation of imagenet classification in [official pytorch release](https://github.com/pytorch/examples/tree/master/imagenet).  Please refer to the official repo for details of data preparations and hardware configurations.

- install [pytorch 0.3](http://pytorch.org)

- clone this repo: `git clone https://github.com/zhirongw/lemniscate.pytorch`

- Training on ImageNet:

  `python main.py DATAPATH --arch resnet18 --nce-k 4096 -nce-t 0.07  --lr 0.03 --nce-m --low-dim 128 -b 256 `

  - parameter nce-k controls the number of negative samples. If nce-k sets to 0, the code also supports full softmax learning.
  - nce-t controls temperature of the distribution. 0.07-0.1 works well in practice.
  - nce-m stabilizes the learning process. A value of 0.5 works well in practice.
  - learning rate is initialized to 0.03, a bit smaller than standard supervised learning.
  - the embedding size is controlled by the parameter low-dim.

- During training, we monitor the supervised validation accuracy by K nearest neighbor with K=1, as it's faster, and gives a good estimation of the feature quality.

- Testing on ImageNet:

  `python main.py DATAPATH --arch resnet18 --resume input_model.pth.tar -e` runs testing with default K=200 neighbors.


