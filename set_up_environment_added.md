This file provides detailed steps for correctly installing and setting up the repository. **It is recommended to read it thoroughly to ensure a proper installation process and avoid potential issues.**

IMPORTANT INFORMATION: The project remains unfinished, which prevented the act of testing an architectura in the dataset FoodSeg103 from being completed. However, the outlined steps represent the correct approach to follow for further progress.

Run the following commands in a Kaggle notebook with GPU enabled. To activate it, go to Settings -> Accelerator and select the GPU option.

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
mim install mmsegmentation==0.30.0 && \
pip install ftfy regex &&  \
cd FoodSeg103-Benchmark-v1 && python tools/test.py checkpoints_folder/SETR_Naive_768x768_80k_base.py  /kaggle/input/checkpoints/checkpoints/SETR_Naive_ReLeM/iter_80000.pth --eval mIoU
