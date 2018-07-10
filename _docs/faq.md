---
docid: faq
title: FAQ / Troubleshooting Help
layout: docs
permalink: /docs/faq.html
---

* [What operating systems are supported?](#what-operating-systems-are-supported)
* [What languages does Caffe2 support?](#what-languages-does-caffe2-support)
* [How do I use Caffe2 with my GPU?](#how-do-i-use-caffe2-with-my-gpu)
* [What are all of these optional libraries used for?](#what-are-all-of-these-optional-libraries-used-for)
* [What is the cmake output?](#what-is-the-cmake-output)
* [Why do I get import errors in Python when I try to use Caffe2?](#why-do-i-get-import-errors-in-python-when-i-try-to-use-caffe2)
  * [How do Python installations work?](#null__how-do-python-installations-work)
* [Why isn't Caffe2 working as expected in Anaconda?](#why-is-caffe2-not-working-as-expected-in-anaconda)
* [How do I fix error messages that are protobuf related?](#how-do-i-fix-error-messages-that-are-protobuf-related)
* [How can I find a file, library, or package on my computer?](#how-can-i-find-a-file-library-or-package-on-my-computer)
* [How can I find what dependencies my Caffe2 library (or other library) has?](#how-can-i-find-what-dependencies-my-caffe2-library-or-other-library-has)
* [The source directory does not contain a CMakeLists.txt file](#the-source-directory-does-not-contain-a-cmakeliststxt-file)
* [No module named caffe2_pybind11_state_gpu](#no-module-named-caffe2pybind11stategpu)
* [My python kernel keeps crashing when using Jupyter](#my-python-kernel-keeps-crashing-when-using-jupyter)
* [I still have a question, where can I get more help?](#i-still-have-a-question-where-can-i-get-more-help)

## What operating systems are supported?

Caffe2 is tested on

* macOS Sierra or above
* Ubuntu 14.04 and 16.04
* CentOS 7
* Windows 10
* iOS and Android
* Raspberry Pi
* Nvidia Tegra

We try to support other operating systems not included in the above list. The above list is what we test every PR on.

## What languages does Caffe2 support?

Caffe2 is written in C++ with a Python frontend. You can find all of the code on our [Github page](https://github.com/pytorch/pytorch).

## How do I use Caffe2 with my GPU?

Many of Caffe2's operators have CUDA implementations, allowing you to use Caffe2 with your Nvidia GPU. To install Caffe2 with GPU support, first install all the needed Nvidia libraries ([CUDA](https://developer.nvidia.com/cuda-downloads) and CuDNN) and then follow the [installation instructions](https://caffe2.ai/docs/getting-started.html).

## What are all of these optional libraries used for?

Caffe2 can has many optional dependencies, which extend Caffe2's core functionality.

----|-----
[cuDNN](https://developer.nvidia.com/cudnn) | If using GPU, this is needed for Caffe2's cuDNN operators
[Eigen 3](http://eigen.tuxfamily.org/) | The default BLAS backend
[LevelDB](https://github.com/google/leveldb) | One of the DB options for storing Caffe2 models
[Nvidia CUDA](https://developer.nvidia.com/cuda-zone) | v6.5 or greater
[OpenCV](http://opencv.org/) | for image-related operations; requires leveldb <= v1.19
[OpenMPI](http://www.open-mpi.org/) | for MPI-related Caffe2 operators, which are used for distributed training
[RocksdB](http://rocksdb.org) | for Caffe2's RocksDB IO backend
[ZeroMQ](http://zeromq.org/) | needed for Caffe2's ZmqDB IO backend (serving data through a socket)
[Graphviz](http://www.graphviz.org/) | Used for plotting in the Jupyter Notebook Tutorials
[Hypothesis](https://hypothesis.readthedocs.io/) | Used in all of the tests
[Jupyter](https://ipython.org/) | Used for interactive python notebooks
[LevelDB](https://github.com/google/leveldb) | One of the DB options for storing Caffe2 models
[lmdb](https://lmdb.readthedocs.io/en/release/) | One of the DB options for storing Caffe2 models
[Matplotlib](http://matplotlib.org/) | Used for plotting in the Jupyter Notebook Tutorials
[Pydot](https://pypi.python.org/pypi/pydot) | Used for plotting in the Jupyter Notebook Tutorials
[Python-nvd3](https://pypi.python.org/pypi/python-nvd3/) | Used for plotting in the Jupyter Notebook Tutorials
[pyyaml](http://pyyaml.org/) | Used in the MNIST tutorial
[requests](http://docs.python-requests.org/en/master/) | Used in the MNIST tutorial to download the dataset
[Scikit-Image](http://scikit-image.org/) | Used for image processing
[SciPy](https://www.scipy.org/) | Used for assorted mathematical operations
[ZeroMQ](http://zeromq.org/) | needed for Caffe2's ZmqDB IO backend (serving data through a socket)


## What is the cmake output?

The cmake output looks like this

```
--
-- ******** Summary ********
-- General:
--   CMake version         : 3.11.2
--   CMake command         : /usr/local/Cellar/cmake/3.11.2/bin/cmake
--   Git version           : v0.1.11-9229-g972440bea
--   System                : Darwin
--   C++ compiler          : /usr/local/opt/ccache/libexec/g++
--   C++ compiler version  : 9.1.0.9020039
--   BLAS                  : Eigen
--   CXX flags             :  -Wno-deprecated -fvisibility-inlines-hidden -Wno-deprecated-declarations -DONNX_NAMESPACE=onnx_c2 -O2 -fPIC -Wno-narrowing -Wall -Wextra -Wno-missing-field-initializers -Wno-type-limits -Wno-unknown-pragmas -Wno-sign-compare -Wno-unused-parameter -Wno-unused-variable -Wno-unused-function -Wno-unused-result -Wno-error=deprecated-declarations -faligned-new
--   Build type            : Release
--   Compile definitions   :
--   CMAKE_PREFIX_PATH     : /Users/hellemn/anaconda3/envs/setup
--   CMAKE_INSTALL_PREFIX  : /Users/hellemn/anaconda3/envs/setup
--
--   BUILD_CAFFE2          : ON
--   BUILD_ATEN            : OFF
--   BUILD_BINARY          : OFF
--   BUILD_CUSTOM_PROTOBUF : ON
--     Link local protobuf : ON
--   BUILD_DOCS            : OFF
--   BUILD_PYTHON          : ON
--     Python version      : 3.6.6
--     Python executable   : /Users/hellemn/anaconda3/envs/setup/bin/python
--     Python includes     : /Users/hellemn/anaconda3/envs/setup/include/python3.6m
--     Python site-packages: lib/python3.6/site-packages
--   BUILD_SHARED_LIBS     : ON
--   BUILD_TEST            : OFF
--   USE_ASAN              : OFF
--   USE_ATEN              : OFF
--   USE_CUDA              : OFF
--   USE_ROCM              : OFF
--   USE_EIGEN_FOR_BLAS    : ON
--   USE_FFMPEG            : OFF
--   USE_GFLAGS            : OFF
--   USE_GLOG              : OFF
--   USE_GLOO              : OFF
--   USE_LEVELDB           : OFF
<more output omitted>
```

You can find it by searching for the string "Summary". If you build Caffe2 from source then there is cmake output somewhere. If you used `setup.py` or `scripts/build_anaconda.sh` then those scripts called cmake, so there is still this output. This output is the most important information for us on most Github issues, so please include it whenever you open an issue.


## Why do I get import errors in Python when I try to use Caffe2?

You will get errors like ```ModuleNotFoundError: No module named <packagename>``` if the Python interpreter that you are running can not find the module that you are trying to import (a Python module is a Python source file or a directory of Python source files). This is always caused by one of the following problems

1. The needed package is not installed
2. The needed package is installed in the wrong place
3. The wrong Python is being used

Follow this quick checklist to debug the problem:

1. If you are trying to run a tutorial, then make sure you have installed all of the dependencies at the top of the [tutorials](tutorials.html) page.
2. `which python` should not be `/usr/bin/python`
3. `echo "$(which python)/../.."` and `echo "$(which pip)/../.."` should be the exact same
4. Make sure you are using the same Python that you installed with
5. Check that in your [cmake output](#what-is-the-cmake-output):
  - Python executable, includes, and site-packages all point to the same installation
  - CMAKE_INSTALL_PREFIX and CMAKE_PREFIX_PATH both point to your Python installation (unless you are using `/usr/local` Python)
6. Read the next three questions on this FAQ about Python installations.
7. Try again in a brand new environment


### How do Python installations work?

A Python installation consists of a Python executable (just called `python`) and a corresponding set of directories:

* **lib/** where c and c++ libraries are found (.so and .a extensions on Linux, .dylib extensions on Mac)
* **lib/python2.7/site-packages/** where installed Python modules are found (Python modules are just Python source files)
* **include/** where headers for c and c++ libraries are found
* **bin/** where the Python executable itself is found

For example, a typical Python 2.7 installed into /usr/local looks like this:

```
/usr/local/                                     # your python root and CMAKE_INSTALL_PREFIX
  +-- bin/
    +-- python                                  # just a symbolic link to /usr/local/bin/python2
    +-- python2                                 # just a symbolic link to /usr/local/bin/python2.7
    +-- python2.7
    +-- <other executables>
  +-- include/
    +-- <header files for c and c++ libraries>
  +-- lib/
    +-- libcaffe2.so                            # The Caffe2 cpp library
    +-- <other Caffe2 c and c++ libraries>
    +-- <other c and c++ libraries>
    +-- python2.7/
      +-- site-packages/
        +-- caffe2/                             # where compiled Caffe2 python source files are
          +--python/
            +--caffe2_pybind11_state.so         # Another Caffe2 cpp library
        +-- <other installed python modules>
```

There may be multiple Python installations on your machine, but only one can be active at a time. Your current Python is at ```which python``` and your current Python root is thus at "$(which python)/../.." . Safe users of Python have several Python installations on their machine:

**System Python**: All Mac and Linux computers have a system Python installation at ```/usr```, with libraries at ```/usr/lib``` and the Python executable at ```/usr/bin/python```. This system Python installation is needed by your system, so you should not mess with it. Try to avoid installing anything into your system Python. If you ever get a "Permission Denied" when trying to install a Python package, then you are probably installing into your system Python and you should stop what you are doing. **Never use ```sudo``` to install a Python package**, or else you may break your system Python installation. On more recent versions of Python, you may pass ```--user``` flag to pip to install into a separate site-packages in your home directory.

**Homebrew Python**: Many Mac users install Python with Homebrew ```brew install python```, which installs a Python into ```/usr/local``` The installation looks the same as above, but may have a different Python version. It is safe to install into this Python.

**Anaconda Python or virtualenvs**: Anaconda and virtualenv are both Python environment managers. A Python env is a separate Python installation with its own Python version and its own installed Python packages. **We recommend that you do all of your work in a Python env.** An Anaconda Python 3.6 installation with one Python 2.7 env called my_first_env and one Python 3.6 env called my_second_env looks like this:

```
~/anaconda3/
  +-- bin/
     +--
     +-- python                             # just a symlink to ~/anaconda3/bin/python3.6
     +-- python3.6
  +-- include/
  +-- lib/
     +-- <c and c++ libraries installed in the root env>
     +-- python3.6/
        +-- site-packages/
          +-- <python modules installed in the root env>
  +-- envs/
     +-- my_first_env/
        +-- bin/
           +-- pip
           +-- python                       # just a symlink to ~/anaconda3/envs/my_first_env/bin/python2.7
           +-- python2.7
        +-- include/
        +-- lib/
           +-- <c and c++ libraries installed in my_first_env>
           +-- python2.7/
             +-- site-packages/
               +-- <python modules installed in my_first_env>
     +-- my_second_env/
        +-- bin/
           +-- pip
           +-- python                       # just a symlink to ~/anaconda3/envs/my_second_env/bin/python3.6
           +-- python3.6
        +-- include/
        +-- lib/
           +-- <c and c++ libraries installed in my_second_env>
           +-- python3.6/
             +-- site-packages/
               +-- <python modules installed in my_second_env>
```

There are three Python installations in the example above. "Activating" a Python environment just points your system to use a particular Python installation. Note how a Python2.7 env can exist inside a Python3.6 installation. virtualenv works the same way as conda-envs; they just have different syntax on how to activate or deactivate a Python environment. Remember that a different Python env may be activated in each of your bash or terminal windows.

`which python` tells you what your current active Python env is. `which pip` tells you what your current active pip is. **`"$(which pip)/.."` and `"$(which python)/.."` should be the same**; if not then your current env is broken and you should create a new one.


## Why is Caffe2 not working as expected in Anaconda?

1. Anaconda Python has a different search path. Normally, Python searches for imported modules in the current directory, then in its site-packages, and then in $PYTHONPATH. Anaconda Python searches first in the current directory, then in its site-packages, then ALSO searches in the root Anaconda's site-packages, and then searches in $PYTHONPATH. This can give confusing behavior and confuse tools like pip and conda-build. For this reason, we recommend that you **only install into conda envs, never into the root Anaconda python**. 

2. There are several ways to create a conda env.

- `conda create -n some_env` : **Don't use this**, as this creates a brand new env but does NOT install Python or setuptools into the env. This means that if you activate your new env with `source activate some_env` immediately after you create it, then your root env will still be activated. Many build tools, including ours, rely on the Python package `distutils` to know where to install Python files. If you use this method, then `distutils` will still point to the root Anaconda Python instead of your Python env, which might conflict with other flags passed to our cmake system.

- `conda create -n some_env anaconda` : **Don't use this** either. This will install *all* base Anaconda packages into your new env. This is a *lot* of packages, most of which you will not use. This wastes a lot of memory and takes a long time to install. This also makes it harder to install later packages, as dependency resolution is complicated by all the existing packages.

- `conda create -n some_env python=3` : **Always use this**. This will create a new env and install only the minimal packages, including Python setuptools and distutils. If you use this to create all your conda envs and never install packages into your root env then you will have a much better experience with Anaconda.

## How do I fix error messages that are Protobuf related?

Protobuf version mismatch is a common problem. Having different protobuf versions often leads to incompatible headers and libraries. **Upgrading to the latest protobuf is not the solution.** The version of Protobuf used during compile time must match the one used at runtime.

Run these commands to see which Protobuf version is currently visible on your machine.

```bash
which protoc
protoc --version
find $(dirname $(which protoc))/../lib -name 'libproto*'
```

Now find what Protobuf version your Caffe2 installation expects. First [find your Caffe2 library](#how-can-i-find-a-file-library-or-package-on-my-computer), which can have several possible locations depending on your install environment. Then run the following command with ```<your libcaffe2>``` replaced with the location of your Caffe2 library.

For Linux: ```ldd <your libcaffe2>```
For macOS: ```otool -L <your libcaffe2>```

You need the Protobuf versions to match.

For example, on a Mac you might find that your current visible Protobuf is:

```
$ which protoc
/usr/local/bin/protoc
$ protoc --version
libprotoc 3.5.1
$ otool -L /usr/local/lib/libprotobuf.dylib
/usr/local/lib/libprotobuf.dylib:
	/usr/local/opt/protobuf/lib/libprotobuf.15.dylib (compatibility version 16.0.0, current version 16.1.0)
	/usr/lib/libz.1.dylib (compatibility version 1.0.0, current version 1.2.11)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 400.9.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.0.0)
```

but that your Caffe2 installation expects

```
$ otool -L /usr/local/lib/libcaffe2.dylib
@rpath/libcaffe2.dylib (compatibility version 0.0.0, current version 0.0.0)
	@rpath/libprotobuf.14.dylib (compatibility version 15.0.0, current version 15.0.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 400.9.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.0.0)
```

This example would lead to Protobuf errors, as `libprotobuf.14.dylib` which Caffe2 expects is not the same as `libprotobuf.15.dylib` which exists on the machine. In this example, the Protobuf on the machine will have to be downgraded to 3.4.1.


## How can I find a file, library, or package on my computer?

Find libraries, binaries, and other files with the `find` command. On Macs and Linux, the conventional name of a library for a package `mypackage` is `libmypackage.a` or `libmypackage.dylib`. `find` accepts wildcards `*` that match any string of any length. For example

```bash
# Find everything associated with protobuf anywhere
find / -name *protobuf* 2>/dev/null

# Find all protobuf libraries everywhere
find / -name libprotobuf* 2>/dev/null
```

Use `which` in combination with the `--version` flag to find out more about executables on your system. For example

```bash
which python
python --version

which protoc
protoc --version
```

## How can I find what dependencies my Caffe2 library (or other library) has?

**For Linux, Ubuntu and CentOS**

Use `ldd <path to a library>` on libraries (files that end in .so) to find out what other libraries it needs and where it expects to find them. You can find where libraries are with the `find` command above.


**For macOS**

Use `otool -L <path to a library>` on libraries (files that end in .dylib) to find out what other libraries it needs and where it expects to find them. Libraries are usually installed under `/usr/lib`, or `/usr/local/lib` (for Homebrew), or alongside a [Python installation](#why-do-i-get-import-errors-in-python-when-i-try-to-use-caffe2). You can find where libraries are with the `find` command above. 

For example:

```bash
$ otool -L ~/anaconda3/envs/my_caffe2_env/lib/libcaffe2.dylib
/Users/my_username/anaconda3/envs/my_caffe2_env/lib/libcaffe2.dylib:
	@rpath/libcaffe2.dylib (compatibility version 0.0.0, current version 0.0.0)
	/usr/local/lib/libprotobuf.14.dylib (compatibility version 15.0.0, current version 15.0.0)
	@rpath/libmkl_rt.dylib (compatibility version 0.0.0, current version 0.0.0)
	@rpath/libgflags.2.2.dylib (compatibility version 2.2.0, current version 2.2.1)
	/usr/local/lib/libglog.0.dylib (compatibility version 1.0.0, current version 1.0.0)
	/usr/lib/libc++.1.dylib (compatibility version 1.0.0, current version 400.9.0)
	/usr/lib/libSystem.B.dylib (compatibility version 1.0.0, current version 1252.0.0)
```

To find out what "@rpath" is, run otool with `-l` (lowercase L) and pipe that into `grep LC_RPATH -A 3`, e.g.

```bash
$ otool -l ~/anaconda3/envs/my_caffe2_env/lib/libcaffe2.dylib | grep LC_RPATH -A 3
          cmd LC_RPATH
      cmdsize 32
         path @loader_path/ (offset 12)
```

In this example, `@rpath` will evaluate to `@loader_path`, which is essentially the location of the library that you ran otool on (see [dyld](https://developer.apple.com/legacy/library/documentation/Darwin/Reference/ManPages/man1/dyld.1.html)). So, in this example, libcaffe2.dylib will look for libgflags.2.2.dylib in the same folder that libcaffe2.dylib is in.


## The source directory does not contain a CMakeLists.txt file

You need to run `git submodule update --init` in the Caffe2 root directory.


## No module named caffe2_pybind11_state_gpu

If you are not building for GPU then ignore this. If you are building for GPU, then make sure CUDA was found correctly in the output of the `cmake` command that was run to build Caffe2.


## My python kernel keeps crashing when using Jupyter

This happens when you try to call Jupyter server directly (like in a Docker container). Use `sh -c "jupyter notebook ..."` to get around this problem.


## I still have a question, where can I get more help?

For further issues, please post a new issue to our [issue tracker on Github](https://github.com/pytorch/pytorch/issues). 

> If your question is about an error installing Caffe2, then please include the following information in your issue:

* `$(uname -a)`
* Which installation guide you followed.
* What flags you passed to `cmake`
* The full output of your `cmake` command


## Miscellaneous errors

* On Mac, you may need to install [Xcode](https://developer.apple.com/xcode/) or at a minimum xcode command line tools. You can install it by running `xcode-select --install`
* If you experience errors related to confu or PeachPy when running `make install`, then install dependencies of NNPACK: `[sudo] pip install --upgrade git+https://github.com/Maratyszcza/PeachPy` and `[sudo] pip install --upgrade git+https://github.com/Maratyszcza/confu`
* If you get model downloading errors when running in `sudo`, then PYTHONPATH might not be visible in that context. Run `sudo visudo` then add this line: `Defaults    env_keep += "PYTHONPATH"`
* If you encounter "AttributeError: 'module' object has no attribute 'MakeArgument'" when calling `core.CreateOperator` then try removing `caffe2/python/utils` from the directory that you installed Caffe2 in.
* If you see [errors with libdc1394](http://stackoverflow.com/questions/12689304/ctypes-error-libdc1394-error-failed-to-initialize-libdc1394) when opencv is installed, then run `ln /dev/null /dev/raw1394` . That solution is not [persistent](http://stackoverflow.com/questions/31768441/how-to-persist-ln-in-docker-with-ubuntu) so try `sh -c 'ln -s /dev/null /dev/raw1394'` or when instantiating the container use: `--device /dev/null:/dev/raw1394`
