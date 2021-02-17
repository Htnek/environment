# Adding gpu-support for Ubuntu 18.04

## Add NVIDIA package repositories
```bash
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/cuda-ubuntu1804.pin
```
```bash
sudo mv cuda-ubuntu1804.pin /etc/apt/preferences.d/cuda-repository-pin-600
```
```bash
sudo apt-key adv --fetch-keys https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/7fa2af80.pub
```
```bash
sudo add-apt-repository "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu1804/x86_64/ /"
```
```bash
sudo apt-get update
```
```bash
wget http://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
```
```bash
sudo apt install ./nvidia-machine-learning-repo-ubuntu1804_1.0.0-1_amd64.deb
```
```bash
sudo apt-get update
```
## Install NVIDIA driver
```bash
sudo apt-get install --no-install-recommends nvidia-driver-450
```
### Reboot. Check that GPUs are visible using the command: nvidia-smi
```bash
wget https://developer.download.nvidia.com/compute/machine-learning/repos/ubuntu1804/x86_64/libnvinfer7_7.1.3-1+cuda11.0_amd64.deb
```
```bash
sudo apt install ./libnvinfer7_7.1.3-1+cuda11.0_amd64.deb
```
```bash
sudo apt-get update
```
## Install development and runtime libraries (~4GB)
```bash
sudo apt-get install --no-install-recommends \
    cuda-11-0 \
    libcudnn8=8.0.4.30-1+cuda11.0  \
    libcudnn8-dev=8.0.4.30-1+cuda11.0
```

## Install TensorRT. Requires that libcudnn8 is installed above.
```bash
sudo apt-get install -y --no-install-recommends libnvinfer7=7.1.3-1+cuda11.0 \
    libnvinfer-dev=7.1.3-1+cuda11.0 \
    libnvinfer-plugin7=7.1.3-1+cuda11.0
```

# Create the environment tf2
```bash
git clone https://github.com/Htnek/environment.git
```
```bash
conda env create -f environment.yml
```
```bash
conda activate tf2
```
```bash
python -m ipykernel install --user --name=python3
```
# Update environment tf2
```bash
conda activate tf2
```
```bash
conda env update --file environment.yml  --prune
```
# Test if GPU is available
```bash
conda activate tf2
```
```bash
python
```
```bash
import tensorflow as tf
```
```bash
tf.config.list_physical_devices('GPU')
```
