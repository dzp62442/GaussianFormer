# Installation
Our code is tested on the following environment.

## 1. Create conda environment
```bash
GIT_LFS_SKIP_SMUDGE=1 git clone git@github.com:dzp62442/GaussianFormer.git
conda create -n gsformer python=3.8.16
conda activate gsformer
```

## 2. Install PyTorch
```bash
pip install torch==2.0.0 torchvision==0.15.1 torchaudio==2.0.1 --index-url https://download.pytorch.org/whl/cu118
```

## 3. Install packages from MMLab
```bash
pip install openmim
mim install mmcv==2.0.1
mim install mmdet==3.0.0
mim install mmsegmentation==1.0.0
mim install mmdet3d==1.1.1
```

## 4. Install other packages
```bash
pip install spconv-cu117 timm einops jaxtyping
```

## 5. Install custom CUDA ops
```bash
cd model/encoder/gaussian_encoder/ops && pip install -e .
cd model/head/localagg && pip install -e .
# for GaussianFormer-2
cd model/head/localagg_prob && pip install -e .
cd model/head/localagg_prob_fast && pip install -e .
```

## 6. (For GaussianFormer-2) Install pointops
```bash
cd pointops
pip install -e .
```

**注意：**
1. GaussianFormer-2 需要安装 pointops，原作者没有提供，需要从 [point-transformer](https://github.com/POSTECH-CVLab/point-transformer/tree/master/lib) 中将 `pointops` 文件夹放入项目目录中进行安装
2. 若遇到 `THC/THC.h` 报错，将所有的 `#include <THC/THC.h>` 注释掉即可
3. 在 pointops 目录的 `__init__.py` 里添加 `from pointops.functions.pointops import furthestsampling as farthest_point_sampling`

## 7. (Optional) For visualization
```bash
pip install pyvirtualdisplay mayavi matplotlib==3.7.2 PyQt5
```