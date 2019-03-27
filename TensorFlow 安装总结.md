---
title: TensorFlow 安装总结
date: 2019-3-22 12:30:24
tags: 
	- python
	- TensorFlow
	- MachineLearning
toc:
	ture
---


# TensorFlow 安装总结

![TensorFlow 2.0 Logo](http://poatdt87z.bkt.clouddn.com/tensorflow2.0.gif)

## TensorFlow 简介：

TensorFlow 是 Google 公司人工智能团队谷歌大脑（Google Brain）研发和维护的开源深度学习框架，世界上由成千上万个开发者为该项目贡献代码，框架能够随着对深度学习的研究进展及时更新。TensorFlow 核心组件包括：最底层的设备层、内核应用、执行器、分发中心。主要是对张量进行运算，有适用于高阶神经网络的Estimators接口。而且 TensorFlow 可轻松移植到网页端和移动设备上。目前最新版是TensorFlow 1.13.1。

TensorFlow-GPU是TensorFlow的GPU版，能够使用支持NVIDIA CUDA 并行计算技术的显卡进行矢量运算，其训练模型的效率比CPU高几十到上百倍。


<!--more-->

## 并行计算框架安装：

我们打开TensorFlow的官网可以明显的在导航栏找到 Install 页面的入口。

然而相信我，安装TensorFlow并没有官方页面上写的那么简单（特别是喜欢挑战难度安装GPU版本），输入几行代码，坐到旁边喝杯茶刷刷微博，过一会就安装完成了。

因为TensorFlow支持众多平台，首先我们要搞懂TensorFlow到底支持哪些操作系统。

- Ubuntu 16.04 或更高版本（这里可代表Linux家族）
- Windows 7 或更高版本
- macOS 10.12.6 (Sierra) 或更高版本（不支持 GPU）
- Raspbian 9.0 或更高版本

可以看出来常用的操作系统都是支持的。

### 安装Cuda

#### Linux

首先我们看一下linux版的安装步骤

1. 由于GPU版本计算速度更快，所以优先考虑安装GPU版本。我们要查看我们的电脑是否支持GPU版本的硬件。

   > 这里有两个问题：
   >
   > 首先，你的电脑需要配置有NVIDIA的显卡
   >
   > 其次，你的显卡需要在CUDA支持名单里 [GPUSUPPORT](https://developer.nvidia.com/cuda-gpus)

2. 确认了你的GPU在NVIDIA CUDA技术支持名单里之后就可以安装驱动了。

   > 我们可以直接从NVIDIA官方网站找到CUDA[下载链接](https://developer.nvidia.com/cuda-downloads)
   >
   > 根据自己的操作系统版本下载合适的安装包。
   >
   > 另外要注意CUDA并不是版本越高越好，一般情况下CUDA发布版本要低于市面上相关机器学习框架的应用版本，也就是说你下载了一个过高的版本可能无法使用，具体如何选择CUDA版本，下文会有介绍。

3. 

安装显卡驱动和 Cuda：
指定到对应的文件所在位置：
`# cd /usr/tmp/tensorflow-gpu`
（这是我的文件所在的路径）

cd到驱动所在目录：

```
# sh ./NVIDIA-Linux-x86_64-375.66.run
# sh cuda_8.0.61_375.26_linux.run
```

修改配置文件：

`# vi ~/.bashrc`
（vi 命令为在terminal终端中进入文本编辑的方法，有的是vim，有界面还可以gedit ~/.bashrc方法进入）
按Insert键，进入插入模式：

```
#gpu driver 

export CUDA_HOME=/usr/local/cuda-8.0 

exportPATH=/usr/local/cuda-8.0/bin:$PATH 

exportLD_LIBRARY_PATH=/usr/local/cuda-8.0/lib64:$LD_LIBRARY_PATH 

exportLD_LIBRARY_PATH="/usr/local/cuda-8.0/lib:${LD_LIBRARY_PATH}"
```



按 Esc 键， 并输入
`# wq`
表示写入并退出。

修改之后需要激活所修改的配置文件：

`# source ~/.bashrc`
然后重启服务器
`# reboot`
接下来就可以通过查看显卡信息测试驱动是否安装成功：

`# nvidia-smi`
![mem](http://poatdt87z.bkt.clouddn.com/mem.png)
有显示，说明显卡驱动安装成功，继续闯关！

测试CUDA是否安装成功：
`# cd /usr/local/cuda/samples/`
如果安装成功了的话，上面这个文件夹是可以进去的
`# make（这步运行时间比较长，不要以为存在问题）`
`# ./bin/x86_64/linux/release/deviceQuery`

\#./bin/x86_64/linux/release/bandwidthTest
显示 Result = PASS 则测试通过
安装CUDNN
指定到对应的文件所在位置：
`# cd /usr/tmp/tensorflow-gpu`
（这是我的文件所在的路径）

```
$ tar -zxvf cudnn-8.0-linux-x64-v6.0.tgz

$ cd cuda

$ cp include/* /usr/local/cuda-8.0/inlcude/

$ cp lib64/lib* /usr/local/cuda-8.0/lib64/
```



注意驱动和cuda的安装顺序，先安装驱动的话，安装cuda时x-configtion选择N

#### Mac OS和Raspbian

因为该硬件没有NVIDIA的显卡所以压根就不支持CUDA，这里跳过

#### Windows

Windows安装CUDA和安装NVIDIA显卡驱动步骤一致。

下载CUDA安装包，打开解压安装。选择精简版安装，安装程序会自动检测不兼容的软件，然会自己安装，自己注册环境变量，十分简单。

由于国产部分杀毒防护软件敌友不分，在安装完成之后，一定要人工检查一下系统变量，看一下CUDA路径是否被添加到Windows环境变量里。

### 安装cuDNN

安装cuDNN也很简单，首先从 [官方网站](https://developer.nvidia.com/rdp/cudnn-download) 下载cuDNN，这里需要注册NVIDIA账户。

#### Linux

```
安装cudnn:
$ tar -xvzf cudnn-8.0-linux-x64-v6.0.tgz
$ cp -P cuda/include/cudnn.h /usr/local/cuda-8.0/include
$ cp -P cuda/lib64/libcudnn* /usr/local/cuda-8.0/lib64
$ chmod a+r /usr/local/cuda-8.0/include/cudnn.h /usr/local/cuda-8.0/lib64/libcudnn*
```

#### Windows

解压`cudnn-xxx-windowsxx-x64-vx.x.x.xx.zip`文件到cuda安装目录，合并到同名文件夹即可。

## TensorFlow安装

这里通常有两种安装方法：

> 1. 从源代码构建
> 2. 从发行版安装

前者适合追求最新版本，或者需要深度制定TensorFlow的用户，当然你想体验一下一个大型软件从源码到可执行文件的编译过程也可以尝试。

后者适合普通用户，可以直接使用Python 的pip工具安装。

#### Linux 从源码构建

Linux 和 macOS 设置

安装以下构建工具以配置开发环境。

安装 Python 和 TensorFlow 软件包依赖项

[Ubuntu](https://tensorflow.google.cn/install/source#ubuntu)[mac OS](https://tensorflow.google.cn/install/source#mac-os)

```
sudo apt install python-dev python-pip  # or python3-dev python3-pip
```

安装 TensorFlow pip 软件包依赖项（如果使用虚拟环境，请省略 `--user` 参数）：

```
pip install -U --user pip six numpy wheel mock
pip install -U --user keras_applications==1.0.5 --no-deps
pip install -U --user keras_preprocessing==1.0.3 --no-deps
```

这些依赖项列在 `REQUIRED_PACKAGES` 下的 [`setup.py`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/pip_package/setup.py) 文件中。

安装 Bazel

[安装 Bazel](https://docs.bazel.build/versions/master/install.html)，它是用于编译 TensorFlow 的构建工具。

将 Bazel 可执行文件的位置添加到 `PATH` 环境变量中。

安装支持 GPU 的版本（可选，仅限 Linux）

没有针对 macOS 的 GPU 支持版本。

要安装在 GPU 上运行 TensorFlow 所需的驱动程序和其他软件，请参阅 [GPU 支持](https://tensorflow.google.cn/install/gpu)指南。

**注意**：您可以轻松地设置 TensorFlow 的某个支持 GPU 的 [Docker 映像](https://tensorflow.google.cn/install/source#docker_linux_builds)。

下载 TensorFlow 源代码

使用 [Git](https://git-scm.com/) 克隆 [TensorFlow 代码库](https://github.com/tensorflow/tensorflow)：

```
git clone https://github.com/tensorflow/tensorflow.git
cd tensorflow
```

代码库默认为 `master` 开发分支。您也可以检出要构建的[版本分支](https://github.com/tensorflow/tensorflow/releases)：

```
git checkout branch_name  # r1.9, r1.10, etc.
```

要测试源代码树的副本，请对 r1.12 及更早版本运行以下测试（这可能需要一段时间）：

```
bazel test -c opt -- //tensorflow/... -//tensorflow/compiler/... -//tensorflow/contrib/lite/...
```

对于 r1.12 之后的版本（如 `master`），请运行以下命令：

```
bazel test -c opt -- //tensorflow/... -//tensorflow/compiler/... -//tensorflow/lite/...
```

**要点**：如果您在使用最新的开发分支时遇到构建问题，请尝试已知可用的版本分支。

配置构建

通过在 TensorFlow 源代码树的根目录下运行以下命令来配置系统构建：

```
./configure
```

此脚本会提示您指定 TensorFlow 依赖项的位置，并要求指定其他构建配置选项（例如，编译器标记）。以下代码展示了 `./configure` 的示例运行会话（您的会话可能会有所不同）：

查看示例配置会话

配置选项

对于 [GPU 支持](https://tensorflow.google.cn/install/gpu)，请指定 CUDA 和 cuDNN 的版本。如果您的系统安装了多个 CUDA 或 cuDNN 版本，请明确设置版本而不是依赖于默认版本。`./configure` 会创建指向系统 CUDA 库的符号链接，因此，如果您更新 CUDA 库路径，则必须在构建之前再次运行此配置步骤。

对于编译优化标记，默认值 (`-march=native`) 会优化针对计算机的 CPU 类型生成的代码。但是，如果要针对不同类型的 CPU 构建 TensorFlow，请考虑指定一个更加具体的优化标记。要查看相关示例，请参阅 [GCC 手册](https://gcc.gnu.org/onlinedocs/gcc-4.5.3/gcc/i386-and-x86_002d64-Options.html)。

您可以将一些预先配置好的构建配置添加到 `bazel build` 命令中，例如：

- `--config=mkl` - 支持 [Intel® MKL-DNN](https://github.com/intel/mkl-dnn)。
- `--config=monolithic` - 此配置适用于基本保持静态的单体构建。

**注意**：从 TensorFlow 1.6 开始，二进制文件使用 AVX 指令，这些指令可能无法在旧版 CPU 上运行。

构建 pip 软件包

Bazel 构建

仅支持 CPU

使用 `bazel` 构建仅支持 CPU 的 TensorFlow 软件包构建器：

```
bazel build --config=opt //tensorflow/tools/pip_package:build_pip_package
```

GPU 支持

要构建支持 GPU 的 TensorFlow 软件包构建器，请运行以下命令：

```
bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
```

Bazel 构建选项

从源代码构建 TensorFlow 可能会消耗大量内存。如果系统内存有限，请使用以下命令限制 Bazel 的内存消耗量：`--local_resources 2048,.5,1.0`。

[官方 TensorFlow 软件包](https://tensorflow.google.cn/install/pip)是使用 GCC 4 构建的，并使用旧版 ABI。对于 GCC 5 及更高版本，为了使您的构建与旧版 ABI 兼容，请使用 `--cxxopt="-D_GLIBCXX_USE_CXX11_ABI=0"`。兼容 ABI 可确保针对官方 TensorFlow pip 软件包构建的自定义操作继续支持使用 GCC 5 构建的软件包。

构建软件包

`bazel build` 命令会创建一个名为 `build_pip_package` 的可执行文件，此文件是用于构建 `pip` 软件包的程序。例如，以下命令会在 `/tmp/tensorflow_pkg` 目录中构建 `.whl` 软件包：

```
./bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
```

尽管可以在同一个源代码树下构建 CUDA 和非 CUDA 配置，但建议您在同一个源代码树中的这两种配置之间切换时运行 `bazel clean`。

安装软件包

生成的 `.whl` 文件的文件名取决于 TensorFlow 版本和您的平台。例如，使用 `pip install` 安装软件包：

```
pip install /tmp/tensorflow_pkg/tensorflow-version-tags.whl
```

**成功**：TensorFlow 现已安装完毕。

Docker Linux 构建

借助 TensorFlow 的 Docker 开发映像，您可以轻松设置环境，以从源代码构建 Linux 软件包。这些映像已包含构建 TensorFlow 所需的源代码和依赖项。要了解安装说明和[可用映像标记的列表](https://hub.docker.com/r/tensorflow/tensorflow/tags/)，请参阅 TensorFlow [Docker 指南](https://tensorflow.google.cn/install/docker)。

#### Windows 从源码构建

Windows 设置

安装以下构建工具以配置 Windows 开发环境。

安装 Python 和 TensorFlow 软件包依赖项

安装[适用于 Windows 的 Python 3.5.x 或 Python 3.6.x 64 位版本](https://www.python.org/downloads/windows/)。选择 pip 作为可选功能，并将其添加到 `%PATH%` 环境变量中。

安装 TensorFlow pip 软件包依赖项：

```
pip3 install six numpy wheel
pip3 install keras_applications==1.0.5 --no-deps
pip3 install keras_preprocessing==1.0.3 --no-deps
```

这些依赖项列在 `REQUIRED_PACKAGES` 下的 [`setup.py`](https://github.com/tensorflow/tensorflow/blob/master/tensorflow/tools/pip_package/setup.py) 文件中。

安装 Bazel

[安装 Bazel](https://docs.bazel.build/versions/master/install-windows.html)，它是用于编译 TensorFlow 的构建工具。

将 Bazel 可执行文件的位置添加到 `%PATH%` 环境变量中。

安装 MSYS2

为构建 TensorFlow 所需的 bin 工具[安装 MSYS2](https://www.msys2.org/)。如果 MSYS2 已安装到 `C:\msys64` 下，请将 `C:\msys64\usr\bin`添加到 `%PATH%` 环境变量中。然后，使用 `cmd.exe` 运行以下命令：

```
pacman -S git patch unzip
```

安装 Visual C++ 生成工具 2015

安装 Visual C++ 生成工具 2015。此软件包随附在 Visual Studio 2015 中，但可以单独安装：

1. 转到 [Visual Studio 下载页面](https://visualstudio.microsoft.com/vs/older-downloads/)，
2. 选择“可再发行组件和生成工具”，
3. 下载并安装：
   - *Microsoft Visual C++ 2015 Redistributable 更新 3*
   - *Microsoft 生成工具 2015 更新 3*

**注意**：TensorFlow 针对 Visual Studio 2015 更新 3 进行了测试。

安装 GPU 支持（可选）

要安装在 GPU 上运行 TensorFlow 所需的驱动程序和其他软件，请参阅 Windows [GPU 支持](https://tensorflow.google.cn/install/gpu)指南。

下载 TensorFlow 源代码

使用 [Git](https://git-scm.com/) 克隆 [TensorFlow 代码库](https://github.com/tensorflow/tensorflow)（`git` 随 MSYS2 一起安装）：

```
git clone https://github.com/tensorflow/tensorflow.git
cd tensorflow
```

代码库默认为 `master` 开发分支。您也可以检出要构建的[版本分支](https://github.com/tensorflow/tensorflow/releases)：

```
git checkout branch_name  # r1.9, r1.10, etc.
```

**要点**：如果您在使用最新的开发分支时遇到构建问题，请尝试已知可用的版本分支。

配置构建

通过在 TensorFlow 源代码树的根目录下运行以下命令来配置系统构建：

```
python ./configure.py
```

此脚本会提示您指定 TensorFlow 依赖项的位置，并要求指定其他构建配置选项（例如，编译器标记）。以下代码展示了 `python ./configure.py` 的示例运行会话（您的会话可能会有所不同）：

查看示例配置会话

配置选项

对于 [GPU 支持](https://tensorflow.google.cn/install/gpu)，请指定 CUDA 和 cuDNN 的版本。如果您的系统安装了多个 CUDA 或 cuDNN 版本，请明确设置版本而不是依赖于默认版本。`./configure.py` 会创建指向系统 CUDA 库的符号链接，因此，如果您更新 CUDA 库路径，则必须在构建之前再次运行此配置步骤。

**注意**：从 TensorFlow 1.6 开始，二进制文件使用 AVX 指令，这些指令可能无法在旧版 CPU 上运行。

构建 pip 软件包

Bazel 构建

仅支持 CPU

使用 `bazel` 构建仅支持 CPU 的 TensorFlow 软件包构建器：

```
bazel build --config=opt //tensorflow/tools/pip_package:build_pip_package
```

GPU 支持

要构建支持 GPU 的 TensorFlow 软件包构建器，请运行以下命令：

```
bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package
```

Bazel 构建选项

从源代码构建 TensorFlow 可能会消耗大量内存。如果系统内存有限，请使用以下命令限制 Bazel 的内存消耗量：`--local_resources 2048,.5,1.0`。

如果构建支持 GPU 的 TensorFlow，请添加 `--copt=-nvcc_options=disable-warnings` 以禁止显示 nvcc 警告消息。

构建软件包

`bazel build` 命令会创建一个名为 `build_pip_package` 的可执行文件，此文件是用于构建 `pip` 软件包的程序。例如，以下命令会在 `C:/tmp/tensorflow_pkg` 目录中构建 `.whl` 软件包：

```
bazel-bin\tensorflow\tools\pip_package\build_pip_package C:/tmp/tensorflow_pkg
```

尽管可以在同一个源代码树下构建 CUDA 和非 CUDA 配置，但建议您在同一个源代码树中的这两种配置之间切换时运行 `bazel clean`。

安装软件包

生成的 `.whl` 文件的文件名取决于 TensorFlow 版本和您的平台。例如，使用 `pip3 install` 安装软件包：

```
pip3 install C:/tmp/tensorflow_pkg/tensorflow-version-cp36-cp36m-win_amd64.whl
```

**成功**：TensorFlow 现已安装完毕。

使用 MSYS shell 构建

也可以使用 MSYS shell 构建 TensorFlow。做出下面列出的更改，然后按照之前的 Windows 原生命令行 (`cmd.exe`) 说明进行操作。

停用 MSYS 路径转换

MSYS 会自动将类似 Unix 路径的参数转换为 Windows 路径，此转换不适用于 `bazel`。（标签 `//foo/bar:bin` 被视为 Unix 绝对路径，因为它以斜杠开头。）

```
export MSYS_NO_PATHCONV=1
export MSYS2_ARG_CONV_EXCL="*"
```

设置 PATH

将 Bazel 和 Python 安装目录添加到 `$PATH` 环境变量中。如果 Bazel 安装到了 `C:\tools\bazel.exe`，并且 Python 安装到了 `C:\Python36\python.exe`，请使用以下命令设置 `PATH`：

```
# Use Unix-style with ':' as separator
export PATH="/c/tools:$PATH"
export PATH="/c/Python36:$PATH"
```

要启用 GPU 支持，请将 CUDA 和 cuDNN bin 目录添加到 `$PATH` 中：

```
export PATH="/c/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v9.0/bin:$PATH"export PATH="/c/Program Files/NVIDIA GPU Computing Toolkit/CUDA/v9.0/extras/CUPTI/libx64:$PATH"export PATH="/c/tools/cuda/bin:$PATH"
```

#### 使用Python自带的pip包管理工具安装

执行`pip install tensorflow =='x.xx'``pip install tensorflow-gpu ==’x.xx’`

linux 执行`sudo pip install tensorflow =='x.xx'``sudo pip install tensorflow-gpu ==’x.xx’`

## 重点TensorFlow-GPU 与CUDA 及cudnn 版本参照表

| 版本                  | Python 版本 | cuDNN | CUDA |
| :-------------------- | :---------- | :---- | :--- |
| tensorflow_gpu-1.12.0 | 3.5-3.6     | 7     | 9    |
| tensorflow_gpu-1.11.0 | 3.5-3.6     | 7     | 9    |
| tensorflow_gpu-1.10.0 | 3.5-3.6     | 7     | 9    |
| tensorflow_gpu-1.9.0  | 3.5-3.6     | 7     | 9    |
| tensorflow_gpu-1.8.0  | 3.5-3.6     | 7     | 9    |
| tensorflow_gpu-1.7.0  | 3.5-3.6     | 7     | 9    |
| tensorflow_gpu-1.6.0  | 3.5-3.6     | 7     | 9    |
| tensorflow_gpu-1.5.0  | 3.5-3.6     | 7     | 9    |
| tensorflow_gpu-1.4.0  | 3.5-3.6     | 6     | 8    |
| tensorflow_gpu-1.3.0  | 3.5-3.6     | 6     | 8    |
| tensorflow_gpu-1.2.0  | 3.5-3.6     | 5.1   | 8    |
| tensorflow_gpu-1.1.0  | 3.5         | 5.1   | 8    |
| tensorflow_gpu-1.0.0  | 3.5         | 5.1   | 8    |

这里经过测试

| TensorFlow - GPU      | CUDA          | cuDNN                       |
| --------------------- | ------------- | --------------------------- |
| tensorflow_gpu-1.12.0 | CUDA 9.0.176  | cuDNNv7.4.2.24 for cuda 9.0 |
| tensorflow_gpu-1.13.0 | CUDA 10.0.130 | cuDNNv7.4.2.24 for cuda10.0 |