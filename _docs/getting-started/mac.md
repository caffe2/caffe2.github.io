{% capture outro %}{% include_relative getting-started/outro.md %}{% endcapture %}

<block class="mac prebuilt" />

We only support Anaconda packages at the moment. If you do not wish to use Anaconda, then you must build Caffe2 from [source](https://caffe2.ai/docs/getting-started.html?platform=mac&configuration=compile).

### Anaconda packages

We build Mac packages without CUDA support for both Python 2.7 and Python 3.6. To install Caffe2 with Anaconda, simply activate your desired conda environment and run the following command.

```bash
conda install -c caffe2 caffe2
```

> This does NOT include libraries that are necessary to run the tutorials, such as jupyter. See the [tutorials](https://caffe2.ai/docs/tutorials) page for the list of required packages needed to run the tutorials.

NOTE: This will install Caffe2 and all of its required dependencies into the current conda environment. We strongly suggest that you create a new conda environment and install Caffe2 into that. A conda environment is like a separate python installation and so won't have problems with your other conda environments. You can learn more about conda environments [here](https://conda.io/docs/user-guide/tasks/manage-environments.html).

### Prebuilt Caffe2 Python Wheel

This is in beta mode, but you can try

```bash
pip install caffe2
```


<block class="mac compile" />

To compile Caffe2 to use your GPU, follow [these](#gpu-support) instructions first, then:

First install your dependencies. You will need [brew](https://brew.sh/) to install Caffe2's dependencies.

```bash
brew install \
    automake \
    cmake \
    git \
    gflags \
    glog \
    python

pip install --user \
    future \
    numpy \
    protobuf \
    pyyaml \
    six
```

> To run the tutorials you will need to install more packages, see the [Tutorial](https://caffe2.ai/docs/tutorials) page for full requirements.


Then compile Caffe2 from source:

```bash
git clone https://github.com/pytorch/pytorch.git && cd pytorch
git submodule update --init --recursive
python setup.py install
```

For any problems, see our [troubleshooting guide](faq.html).


## Test the Caffe2 Installation
Run this to see if your Caffe2 installation was successful. 

```bash
cd ~ && python -c 'from caffe2.python import core' 2>/dev/null && echo "Success" || echo "Failure"
```

If this fails, then get a better error message by running Python in your home directory and then running `from caffe2.python import core` inside Python. Then see the [Troubleshooting](faq.html) page for help.

## GPU Support

In the instance that you have a NVIDIA supported GPU in your Mac, then you should visit the NVIDIA website for [CUDA](https://developer.nvidia.com/cuda-downloads) and [cuDNN](https://developer.nvidia.com/cudnn) and install the provided binaries. Also see this [Nvidia guide](http://docs.nvidia.com/cuda/cuda-installation-guide-mac-os-x/) on setting up your GPU correctly. Caffe2 requires CUDA 6.5 or greater.

Once CUDA and CuDNN (and optionally NCCL) are installed, please verify that your CUDA installation is working as expected, and then continue with your preferred Caffe2 installation path. 

After Caffe2 is installed, you should NOT see the following error when you try to import caffe2.python.core in Python

```bash
WARNING:root:This caffe2 python run does not have GPU support. Will run in CPU only mode.
WARNING:root:Debug message: No module named 'caffe2.python.caffe2_pybind11_state_gpu'
```

If you see this error then your GPU installation did not work correctly.

{{ outro | markdownify }}

<block class="mac docker" />

<block class="mac cloud" />
