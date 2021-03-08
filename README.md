# Latent Composition
[Project Page](./) |  [Paper](./) 


<img src='img/teaser.jpeg' width=600>  

Using latent space regression to analyze and leverage compositionality in GANs.\
[Lucy Chai](http://people.csail.mit.edu/lrchai/), [Jonas Wulff](http://people.csail.mit.edu/jwulff/), [Phillip Isola](http://web.mit.edu/phillipi/)

## Prerequisites
- Linux
- Python 3
- CPU or NVIDIA GPU + CUDA CuDNN

**Table of Contents:**<br>
1. [Setup](#setup)<br>
3. [Colab](#colab) - run it in your browser without installing anything locally<br>
2. [Pretrained Models](#pretrained) - quickstart with pretrained models<br>
3. [Notebooks](#notebooks) - jupyter notebooks for interactive composition<br>
4. [Training](#training) - pipeline for training encoders<br>

<a name="colab"/>

## Colab

TODO

<a name="setup"/>

## Setup

- Clone this repo:
```bash
git clone https://github.com/chail/latent-composition.git
```

- Install dependencies:
	- we provide a Conda `environment.yml` file listing the dependencies. You can create a Conda environment with the dependencies using:
```bash
conda env create -f environment.yml
```

- Download resources:
	- we provide a script for downloading associated resources and pretrained models. Fetch these by running:
```bash
bash resources/download_resources.sh
```

<a name="pretrained"/>
## Quickstart with pretrained models

See the following code snippet for a basic example. An notebook format is provided in `notebooks/quickstart.ipynb`

```python
from networks import networks

nets = networks.define_nets('proggan', 'celebahq')
# proggan: celebahq, livingroom, church
# stylegan: ffhq, church, car, horse

with torch.no_grad():
    im = nets.seed2image(1,seed=10)
    hints, mask = masking.mask_upsample(im)
    rec = nets.invert(hints, mask=mask)
```

<a name="notebooks"/>
## Notebooks

First, setup symlinked required for notebooks: `bash notebooks/setup_notebooks.sh`. Add the conda environment to jupyter kernels: `python -m ipykernel install --user --name latent-composition`. 

We provide a few interactive examples:
1. `quickstart.ipynb`: basic usage example
2. `interactive-masking.ipynb`: investigate GAN priors from incomplete images
3. `interactive-composition.ipynb`: compose multiple images
4. `finetune-and-edit.ipynb`: finetune the model on a real image, and then compose in real-time


<a name="training"/>
## Training

Coming soon!


### TODOs
- [ ] Add experiment scripts
- [ ] Add training code
- [ ] Webpage of random samples

### Acknowledgements

We thank the authors of these repositories:
- [Gan Seeing](https://github.com/davidbau/ganseeing) for GAN and visualization utilities
- [StyleGAN 2 Pytorch](https://github.com/rosinality/stylegan2-pytorch) for pytorch implementation of StyleGAN 2 and pretrained models
- [Pixel2Style2Pixel](https://github.com/eladrich/pixel2style2pixel) for identity loss implementation
- [Pytorch FID](https://github.com/mseitzer/pytorch-fid) for FID implementation

### Citation
If you use this code for your research, please cite our paper:
```
@inproceedings{chai2021latent,
  title={Using latent space regression to analyze and leverage compositionality in GANs},
  author={Chai, Lucy and Wulff, Jonas and Isola, Phillip},
  booktitle={International Conference on Learning Representations},
  year={2021}
 }
```

