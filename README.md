# SlowFastNetworks
PyTorch implementation of ["SlowFast Networks for Video Recognition"](https://arxiv.org/abs/1812.03982).

## Setup
### Environment
```bash
conda env create -f environment.yml
conda activate slowfastnet
```
### Download UCF 101
```bash
wget https://www.crcv.ucf.edu/data/UCF101/UCF101.rar
export DATA_DIR=<YOUR_DATA_DIR>
unrar x UCF101.rar $DATA_DIR
```
### Split into train/validation
```bash
export N_valid=30 # number of videos in validatation set per class
mv $DATA_DIR/UCF-101/ $DATA_DIR/train
mkdir $DATA_DIR/validation
for dir in $(ls $DATA_DIR/train); do mkdir $DATA_DIR/validation/$dir; shuf -zn$N_valid -e $DATA_DIR/train/$dir/*.avi | xargs -0 -I{} mv -v {} $DATA_DIR/validation/$dir; done
```
## Train
1. Dataset should be orgnized as：
```
dataset(e.g. UCF-101)
│    │ train
│    │    │ ApplyEyeMakeup
│    │    │ ApplyLipstick
│    │    │ ...
│    │ validation
│    │    │ ApplyEyeMakeup
│    │    │ ApplyLipstick
│    │    │ ...
```

2. Modify the params in config.py (i.e. set `params['dataset']` to `<YOUR_DATA_DIR>` )

## Code Reference:
[1] https://github.com/Guocode/SlowFast-Networks/
[2] https://github.com/jfzhang95/pytorch-video-recognition
[3] https://github.com/irhumshafkat/R2Plus1D-PyTorch
