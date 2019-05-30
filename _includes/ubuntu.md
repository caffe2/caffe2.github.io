{% capture outro %}{% include outro.md %}{% endcapture %}

<block class="ubuntu prebuilt" />

We only support Anaconda packages at the moment. If you do not wish to use Anaconda, then you must build Caffe2 from [source](https://caffe2.ai/docs/getting-started.html?platform=ubuntu&configuration=compile).

### Anaconda packages

We build Linux packages without CUDA support, with CUDA 9.0 support, and with CUDA 8.0 support, for both Python 2.7 and Python 3.6. These packages are built on Ubuntu 16.04, but they will probably work on Ubuntu14.04 as well (if they do not, please tell us by creating an issue on our [Github page](https://github.com/pytorch/pytorch/issues)). To install Caffe2 with Anaconda, simply activate your desired conda environment and then run one of the following commands:

If you do not have a GPU:

```bash
conda install pytorch-nightly-cpu -c pytorch
```

For GPU support you will need [CUDA](https://developer.nvidia.com/cuda-downloads), [CuDNN](https://developer.nvidia.com/cudnn), and [NCCL](https://developer.nvidia.com/nccl). These must be installed from Nvidia's website. 

For Caffe2 with CUDA 9 and CuDNN 7 support:

```bash
conda install pytorch-nightly -c pytorch
```

For Caffe2 with CUDA 8 and CuDNN 7 support:

```bash
conda install pytorch-nightly cuda80 -c pytorch
```

> This does NOT include libraries that are necessary to run the tutorials, such as jupyter. See the [tutorials](https://caffe2.ai/docs/tutorials) page for the list of required packages needed to run the tutorials.

NOTE: This will install Caffe2 and all of its required dependencies into the current conda environment. We strongly suggest that you create a new conda environment and install Caffe2 into that. A conda environment is like a separate python installation and so won't have problems with your other conda environments. You can learn more about conda environments [here](https://conda.io/docs/user-guide/tasks/manage-environments.html).


<block class="ubuntu cloud" />
You can easily try out Caffe2 by using the Cloud services. Caffe2 is available as AWS (Amazon Web Services) Deep Learning AMI and Microsoft Azure Virtual Machine offerings. You can run run Caffe2 in the Cloud at any scale.

* [AWS Deep Learning AMI (Ubuntu)](https://aws.amazon.com/marketplace/pp/B06VSPXKDX?qid=1489099515180&sr=0-6&ref_=srh_res_product_title)
* [Microsoft Azure Data Science Virtual Machine for Linux (Ubuntu)](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/microsoft-ads.linux-data-science-vm-ubuntu?tab=Overview)

<block class="ubuntu compile" />

We test the latest code on

* Ubuntu 14.04
* Ubuntu 16.04

### Install Dependencies

```bash
sudo apt-get update
sudo apt-get install -y --no-install-recommends \
      build-essential \
      git \
      libgoogle-glog-dev \
      libgtest-dev \
      libiomp-dev \
      libleveldb-dev \
      liblmdb-dev \
      libopencv-dev \
      libopenmpi-dev \
      libsnappy-dev \
      libprotobuf-dev \
      openmpi-bin \
      openmpi-doc \
      protobuf-compiler \
      python-dev \
      python-pip                          
pip install --user \
      future \
      numpy \
      protobuf \
      typing \
      hypothesis
```

> Note `libgflags2` is for Ubuntu 14.04. `libgflags-dev` is for Ubuntu 16.04.

```bash
# for Ubuntu 14.04
sudo apt-get install -y --no-install-recommends \
      libgflags2 \
      cmake3
# for Ubuntu 16.04
sudo apt-get install -y --no-install-recommends \
      libgflags-dev \
      cmake
```

> If you have a GPU, follow [these additional steps](#install-with-gpu-support) before continuing.

### Clone & Build

```bash
git clone https://github.com/pytorch/pytorch.git && cd pytorch
git submodule update --init --recursive
python setup.py install
```

### Test the Caffe2 Installation
Run this to see if your Caffe2 installation was successful. 

```bash
cd ~ && python -c 'from caffe2.python import core' 2>/dev/null && echo "Success" || echo "Failure"
```

If this fails, then get a better error message by running Python in your home directory and then running `from caffe2.python import core` inside Python.

If this fails with a message about not finding caffe2.python or not finding libcaffe2.so, please see [this info](faq.html#why-do-i-get-import-errors-in-python-when-i-try-to-use-caffe2) on how Caffe2 installs in Python.

If you installed with GPU support, test that the GPU build was a success with this command (run from the top level pytorch directory). You will get a test output either way, but it will warn you at the top of the output if CPU was used instead of GPU, along with other errors such as missing libraries.

```bash
python caffe2/python/operator_test/activation_ops_test.py
```

<block class="ubuntu compile" />
### Install with GPU Support

If you plan to use GPU instead of CPU only, then you should install NVIDIA CUDA 8 and cuDNN v5.1 or v6.0, a GPU-accelerated library of primitives for deep neural networks.
[NVIDIA's detailed instructions](http://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#ubuntu-installation) or if you're feeling lucky try the quick install set of commands below.

**Update your graphics card drivers first!** Otherwise you may suffer from a wide range of difficult to diagnose errors.

**For Ubuntu 14.04**

```bash
sudo apt-get update && sudo apt-get install wget -y --no-install-recommends
wget "http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1404/x86_64/cuda-repo-ubuntu1404_8.0.61-1_amd64.deb"
sudo dpkg -i cuda-repo-ubuntu1404_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```

**For Ubuntu 16.04**

```bash
sudo apt-get update && sudo apt-get install wget -y --no-install-recommends
wget "http://developer.download.nvidia.com/compute/cuda/repos/ubuntu1604/x86_64/cuda-repo-ubuntu1604_8.0.61-1_amd64.deb"
sudo dpkg -i cuda-repo-ubuntu1604_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```

#### Install cuDNN (all Ubuntu versions)

**Version 5.1**
```
CUDNN_URL="http://developer.download.nvidia.com/compute/redist/cudnn/v5.1/cudnn-8.0-linux-x64-v5.1.tgz"
wget ${CUDNN_URL}
sudo tar -xzf cudnn-8.0-linux-x64-v5.1.tgz -C /usr/local
rm cudnn-8.0-linux-x64-v5.1.tgz && sudo ldconfig
```

**Version 6.0**
Visit [NVIDIA's cuDNN download](https://developer.nvidia.com/rdp/cudnn-download) to register and download the archive. Follow the same instructions above switching out for the updated library.

Be warned that installing CUDA and CuDNN will increase the size of your build by about 4GB, so plan to have at least 12GB for your Ubuntu disk size.

### Setting Up Tutorials & Jupyter Server

If you're running this all on a cloud computer, you probably won't have a UI or way to view the IPython notebooks by default. Typically, you would launch them locally with `ipython notebook` and you would see a localhost:8888 webpage pop up with the directory of notebooks running. The following example will show you how to launch the Jupyter server and connect to remotely via an SSH tunnel.

First configure your cloud server to accept port 8889, or whatever you want, but change the port in the following commands. On AWS you accomplish this by adding a rule to your server's security group allowing a TCP inbound on port 8889. Otherwise you would adjust iptables for this.

![security group screenshot](../static/images/security-group-jupyter.png)

Next you launch the Juypter server.

```
jupyter notebook --no-browser --port=8889
```

Then create the SSH tunnel. This will pass the cloud server's Jupyter instance to your localhost 8888 port for you to use locally. The example below is templated after how you would connect AWS, where `your-public-cert.pem` is your own public certificate and `ubuntu@super-rad-GPU-instance.compute-1.amazonaws.com` is your login to your cloud server. You can easily grab this on AWS by going to Instances > Connect and copy the part after `ssh` and swap that out in the command below.

```
ssh -N -f -L localhost:8888:localhost:8889 -i "your-public-cert.pem" ubuntu@super-rad-GPU-instance.compute-1.amazonaws.com
```


{{ outro | markdownify }}

<block class="ubuntu docker" />

<block class="ubuntu cloud" />
