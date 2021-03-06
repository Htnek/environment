# How to get Tensorflow working with Anaconda on Windows
```bash
conda install cudatoolkit==10.1.243 cudnn tensorflow-gpu
```
# Adding NVIDIA GPU support for Ubuntu 18.04
This is from https://www.tensorflow.org/install/gpu

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
### Reboot. Check that GPUs are visible using the command:
```bash
nvidia-smi
```
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
# Install Anaconda
Download installer from:
https://www.anaconda.com/download/#linux

Include the bash command regardless of whether or not you are using Bash shell.  
If you did not download to your Downloads directory, replace ~/Downloads/ with the path to the file you downloaded.
```bash
bash ~/Downloads/Anaconda3-YYYY.MM-Linux-x86_64.sh
```
Scroll to the bottom of the license terms and enter “Yes” to agree.  
Accept the default install location.  
The installer prompts “Do you wish the installer to initialize Anaconda3 by running conda init?” Choose “yes”.  
Close and open your terminal window for the installation to take effect, or you can enter the command:
```bash
source ~/.bashrc
```
To run conda from anywhere without having the base environment activated by default, use:
```bash
conda config --set auto_activate_base False
```
## Create the environment tf2
```bash
git clone https://github.com/Htnek/environment.git
```
```bash
conda env create -f environment.yml
```
```bash
conda activate tf2
```
## Registering kernel
```bash
python -m ipykernel install --user --name=python3
```
## Removing unwanted-kernel
Find it with:
```bash
jupyter kernelspec list
```
Remove it with:
```bash
jupyter kernelspec uninstall unwanted-kernel
```
## Starting Jupyter Notebook
```bash
jupyter notebook
```
## Update environment tf2
```bash
conda env update --file environment.yml  --prune
```
## Removing environment
Show name of environment
```bash
conda info --envs
```
Removal of environment
```bash
conda remove --name name_of_environment --all
```

# Test if GPU is available
Start a terminal
```bash
conda activate tf2
```
Start python
```bash
python
```
In python write:
```bash
import tensorflow as tf
```
In python write:
```bash
tf.config.list_physical_devices('GPU')
```
If all goes well you will see:   
  
>Adding visible gpu devices: 0  
>[PhysicalDevice(name='/physical_device:GPU:0', device_type='GPU')]  

# How to watch GPU usage
```bash
watch -n 1 nvidia-smi
```
