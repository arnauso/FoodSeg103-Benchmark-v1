# FoodSeg103 Benchmark Setup and Installation Guide

This file provides detailed steps for correctly installing and setting up the repository. **It is recommended to read it thoroughly to ensure a proper installation process and avoid potential issues.**

## Important Information

The project remains unfinished, which prevented testing an architecture on the FoodSeg103 dataset from being completed. However, the outlined steps represent the correct approach for further progress.

---

## Previous Steps

1. **Download Dataset**: Download the FoodSeg103 dataset from [DatasetNinja](https://datasetninja.com/food-seg-103) and upload it to your Kaggle datasets.

2. **Download Checkpoints**: Obtain pretrained checkpoints for architectures from the *Benchmark and Model Zoo* section of the repository's README, or use these Kaggle datasets:
    - [FoodSeg103 Dataset](https://www.kaggle.com/datasets/andreurosca/foodseg103)
    - [UNIMIB 2016 Dataset](https://www.kaggle.com/datasets/andreurosca/unimib-2016-official)
    - [Checkpoints](https://www.kaggle.com/datasets/andreurosca/checkpoints)
    - [Swin-Small Model Config](https://www.kaggle.com/datasets/andreurosca/swin-small-patch4-window7-224-22k)
    - [Demo File](https://www.kaggle.com/datasets/andreurosca/pspnet-r50-d8-512x1024-40k-cityscapes-continue-pth)

3. **Enable GPU on Kaggle**: In your Kaggle notebook, activate the GPU by navigating to *Settings -> Accelerator* and selecting the GPU option.

```bash
#1) Create conda environment with Python 3.7 inside Kaggle
!conda create -n foodseg python=3.7 -y

#2) Activate conda environment, git clone the repo, install torch and mmcv version
!source /opt/conda/bin/activate foodseg && \
rm -rf FoodSeg103-Benchmark-v1 && \
git clone --recursive https://github.com/arnauso/FoodSeg103-Benchmark-v1 && \
cd FoodSeg103-Benchmark-v1 && \
pip install -r requirements.txt && \
pip install torch==1.8.2 torchvision==0.9.2 torchaudio==0.8.2 --extra-index-url https://download.pytorch.org/whl/lts/1.8/cu111 && pip install -U openmim && \
mim install "mmcv==2.1.0"

#3) Activate conda environment,install mmsegmentation, try to test architecture with the checkpoint downloaded iter_80000.pth
!source /opt/conda/bin/activate foodseg && python --version && \
rm -rf FoodSeg103-Benchmark-v1 && \
git clone --recursive https://github.com/arnauso/FoodSeg103-Benchmark-v1 && \
mim install mmsegmentation==0.30.0 && \
pip install ftfy regex &&  \
cd FoodSeg103-Benchmark-v1 && python tools/test.py checkpoints_folder/SETR_Naive_768x768_80k_base.py  /kaggle/input/checkpoints/checkpoints/SETR_Naive_ReLeM/iter_80000.pth --eval mIoU
