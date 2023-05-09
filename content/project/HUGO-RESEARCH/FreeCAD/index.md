---
title: FreeCAD官网相关文档翻译-1_Compile_on_Linux
summary: FreeCAD官网相关文档翻译第一章节
tags:
  - Deepin
  - CAD
date: 2022-10-21
#external_link: https://bbs.deepin.org/zh/post/244550
---
今天看到个关于**Free CAD**的文章，然后试着翻译一下：

原文：[https://wiki.freecadweb.org/Compile_on_Linux](https://wiki.freecadweb.org/Compile_on_Linux)

> 这里有一个正在为FreeCAD的开发进行测试的实验性FreeCAD Docker容器。更多信息请访问[在Docker上编译](https://wiki.freecadweb.org/Compile_on_Docker)。

# **概述**

在最近的linux发行版上，FreeCAD通常很容易构建，因为所有依赖关系通常都是由包管理器提供的。它主要包括三个步骤：

1.获取FreeCAD源代码。
2.获取FreeCAD所需要的依赖或包。
3.用 `cmake`配置，用 `make`编译。

接下来，将详细解释整个过程、一些[构建脚本](https://wiki.freecadweb.org/Compile_on_Linux#Automatic_build_scripts "build scripts")以及可能遇到的一些特殊情况。如果您在下面的文本中发现任何错误或过时的内容(Linux发行版经常更改)，或者您所使用的发行版没有列出，请在[论坛](https://forum.freecadweb.org/index.php)中讨论该问题，并帮助我们纠正它。

![0e1c153e6247a742745d320c9aae8d04_202210201634517905_5F6B68B732722130813906259A0C9FA0.jpg](https://storage.deepin.org/thread/202210210135339520_0e1c153e6247a742745d320c9aae8d04_202210201634517905_5F6B68B732722130813906259A0C9FA0.jpg)

图中下方小字翻译：（从源代码编译FreeCAD的一般工作流程。第三方依赖项必须在系统中，FreeCAD源代码同样也是。*CMake对系统进行了配置，通过一个make指令就可以编译整个项目。*）

# 获取源码

**Git**

获取代码的最佳方法是 `clone`只读的[Git存储库](https://github.com/FreeCAD/FreeCAD)。为此，您需要 `git`程序，它可以在大多数Linux发行版中轻松地安装。也可以从[官方网站](http://git-scm.com/)获取。
Git可以通过以下命令安装（在Linux上）：

```
sudo apt install git
```

下面的命令将把最新版本的FreeCAD源代码副本放在一个名为 `freecad-source`的新目录中。

```
git clone https://github.com/FreeCAD/FreeCAD.git freecad-source
```

**源代码归档**

或者您也可以将源代码作为一个归档文件，一个.zip或.tar.gz文件下载，，并将其解压到所需的目录中。

# 获取依赖

要编译FreeCAD，您必须安装[第三方库](https://wiki.freecadweb.org/Third_Party_Libraries)中提到的必要依赖项；下面列出了不同Linux发行版中包含这些依赖项的包。请注意，库的名称和可用性将取决于您的特定发行版；如果您的发行版是旧的，那么有些包可能不可用或拥有不同的名称。在这种情况下，请查看下面[较老的和非常规的发行版](https://wiki.freecadweb.org/Compile_on_Linux#Older_and_non-conventional_distributions)部分。

安装好所有依赖项之后，进行编译FreeCAD。

请注意FreeCAD的源代码大小约为**500 MB**；如果克隆包含整个修改历史的Git存储库，它可能是它的三倍大小。获取所有依赖项可能需要下载**500 MB**或更多的新文件；当这些文件被解压时，它们可能需要**1500 MB**或更多的空间。还要注意，*当系统复制和修改整个源代码时*，编译过程可能会生成高达**1500 MB**的附加文件。因此，在尝试编译时，请确保您的硬盘中有足够的空闲空间，至少**4 GB**。

**Debian和Ubuntu**
在基于Debian的系统上(Debian, Ubuntu, Mint等)，安装所有需要的依赖是非常容易的。大多数库都可以通过apt或Synaptic包管理器获得。

如果你已经从官方存储库安装了FreeCAD，你可以在终端上用这一行代码安装它的构建依赖：

```
sudo apt build-dep freecad
```

但是，如果存储库中的FreeCAD版本较旧，则依赖项可能不适合编译最新版本的FreeCAD。因此，请检查您是否安装了以下软件包。

这些包对于任何一种的成功编译都是必不可少的:

`build-essential`，安装C和c++编译器、C开发库和make程序。
`cmake`，配置FreeCAD源代码的必备工具。你也可以安装 `cmake-gui`和 `cmake-curses-gui`来作为图形界面的选择。
`Libtool`，生成共享库的必备工具。
`lbs-release`是标准的基础报告实用程序，通常已经安装在Debian系统中，它允许您通过编程区分纯Debian安装还是其他发行版，如Ubuntu或Linux Mint。不要删除此包，因为许多其他系统包可能依赖于它。

FreeCAD的编译使用Python语言，它也在运行时作为脚本语言使用。如果您使用的是基于Debian的发行版，那么Python解释器通常已经安装好了。

`python3`；
`swig`，是创建c++代码和Python之间接口的工具。

请检查您是否安装了**Python 3**。Python 2在2019年被淘汰使用了，所以FreeCAD的新开发没有使用该版本进行测试。

需要安装Boost库:

* `libboost-dev`
* `libboost-date-time-dev`
* `libboost-filesystem-dev`
* `libboost-graph-dev`
* `libboost-iostreams-dev`
* `libboost-program-options-dev`
* `libboost-python-dev`
* `libboost-regex-dev`
* `libboost-serialization-dev`
* `libboost-thread-dev`

Coin库需要安装:

`libcoin80-dev`，用于Debian Jessie, Stretch, Ubuntu 16.04到18.10，或
`libcoin-dev`，适用于Debian Buster, Ubuntu 19.04及更新版本，也适用于Ubuntu 18.04/18.10，其中添加了[freecad-stable/freecad-daily PPAs](https://wiki.freecadweb.org/Installing_on_Linux#Official_Ubuntu_repository)到您的软件源中。

处理数学、三角曲面、排序、网格、计算机视觉、地图投影、3D可视化、X11 窗口系统、XML解析和Zip文件读取的几个库：

* `libeigen3-dev`
* `libgts-bin`
* `libgts-dev`
* `libkdtree++-dev`
* `libmedc-dev`
* `libopencv-dev` or `libcv-dev`
* `libproj-dev`
* `libvtk7-dev` or `libvtk6-dev`
* `libx11-dev`
* `libxerces-c-dev`
* `libzipios++-dev`

> Python 2 和 Qt4
> 
> 不推荐在较新的安装中这样做，因为Python 2和Qt4都已过时。从0.20版本开始，FreeCAD不再支持它们。

**Python 3 和 Qt5**
要编译在Debian Buster、Ubuntu 19.04及更新版本系统上的的FreeCAD，以及添加了[freecad-stable/freecad-daily PPAs](https://wiki.freecadweb.org/Installing_on_Linux#Official_Ubuntu_repository "Installing on Linux")的Ubuntu 18.04/18.10版本的FreeCAD，请安装以下依赖项。

* `qtbase5-dev`
* `qttools5-dev`
* `qt5-default` (if compiling 0.20 on a machine that still has Qt4)
* `libqt5opengl5-dev`
* `libqt5svg5-dev`
* `libqt5webkit5-dev` or `qtwebengine5-dev`
* `libqt5xmlpatterns5-dev`
* `libqt5x11extras5-dev`
* `libpyside2-dev`
* `libshiboken2-dev`
* `pyside2-tools`
* `pyqt5-dev-tools`
* `python3-dev`
* `python3-matplotlib`
* `python3-packaging`
* `python3-pivy`
* `python3-ply`
* `python3-pyside2.qtcore`
* `python3-pyside2.qtgui`
* `python3-pyside2.qtsvg`
* `python3-pyside2.qtwidgets`
* `python3-pyside2.qtnetwork`
* `python3-pyside2.qtwebengine`
* `python3-pyside2.qtwebenginecore`
* `python3-pyside2.qtwebenginewidgets`
* `python3-pyside2.qtwebchannel`
* `python3-pyside2uic`

**OpenCascade 内核**

OpenCascade内核是创建3D形状的核心图形库。它存在于官方版本OCCT和社区版本OCE中。不再推荐社区版本，因为它已经过时了。

对于Debian Buster和Ubuntu 18.10及更新版本的系统，以及添加了[freecad-stable/freecad-daily PPAs](https://wiki.freecadweb.org/Installing_on_Linux#Official_Ubuntu_repository "Installing on Linux")的Ubuntu 18.04，请安装官方软件包。

* `libocct*-dev`
  * `libocct-data-exchange-dev`
  * `libocct-draw-dev`
  * `libocct-foundation-dev`
  * `libocct-modeling-algorithms-dev`
  * `libocct-modeling-data-dev`
  * `libocct-ocaf-dev`
  * `libocct-visualization-dev`
* `occt-draw`

对于Debian Jessie、Stretch、Ubuntu 16.04及更新版本，请安装社区版本包。

* `liboce*-dev`
  * `liboce-foundation-dev`
  * `liboce-modeling-dev`
  * `liboce-ocaf-dev`
  * `liboce-ocaf-lite-dev`
  * `liboce-visualization-dev`
* `oce-draw`

您可以单独安装库，也可以使用星号展开。如果希望安装社区库，则将**occ**更改为**oce**。

```
sudo apt install libocct*-dev
```

**可选包**

你也可以选择安装这些额外的包：

`libsimage-dev`，使Coin支持额外的图像文件格式。
`Doxygen`和 `libcoin-doc` （旧系统则使用 `libcoin80-doc`)，用于生成源代码文档。

`libspnav-dev`，用于支持[3D输入设备](https://wiki.freecadweb.org/3D_input_devices)，如3Dconnexion“Space Navigator”或“Space Pilot”。
`checkinstall`，如果您打算将已安装的文件注册到系统的包管理器中，那么您可以稍后卸载它。
`python3-markdown`，用于插件管理器原生地显示markdown格式的README文件。
`python3-git`，用于插件管理器使用**git**来获取和更新工作台和宏。

***Python 3 and Qt5单行命令***（不确定这个标题是否翻译准确）

需要**Pyside2**在Debian buster和[freecad-stable/freecad-daily PPAs](https://wiki.freecadweb.org/Installing_on_Linux#Official_Ubuntu_repository "Installing on Linux")中可用。

```
sudo apt install cmake cmake-gui libboost-date-time-dev libboost-dev libboost-filesystem-dev libboost-graph-dev libboost-iostreams-dev libboost-program-options-dev libboost-python-dev libboost-regex-dev libboost-serialization-dev libboost-thread-dev libcoin-dev libeigen3-dev libgts-bin libgts-dev libkdtree++-dev libmedc-dev libocct-data-exchange-dev libocct-ocaf-dev libocct-visualization-dev libopencv-dev libproj-dev libpyside2-dev libqt5opengl5-dev libqt5svg5-dev libqt5webkit5-dev libqt5x11extras5-dev libqt5xmlpatterns5-dev libshiboken2-dev libspnav-dev libvtk7-dev libx11-dev libxerces-c-dev libzipios++-dev occt-draw pyside2-tools python3-dev python3-matplotlib python3-packaging python3-pivy python3-ply python3-pyside2.qtcore python3-pyside2.qtgui python3-pyside2.qtsvg python3-pyside2.qtwidgets python3-pyside2.qtnetwork python3-pyside2.qtwebengine python3-pyside2.qtwebenginecore python3-pyside2.qtwebenginewidgets python3-pyside2.qtwebchannel python3-markdown python3-git python3-pyside2uic qtbase5-dev qttools5-dev swig
```

注意:在某些版本的Ubuntu和某些版本的Qt上，你会得到一个**python3-pyside2uic**找不到的错误——在这些系统上你可以安全地忽略它。在Ubuntu 20.04上，你需要添加 `pyqt5-dev-tools`。详情可以在论坛讨论中找到。

**Python 2 and Qt4 单行命令**（不确定这个标题是否翻译准确）

不建议在较新的安装中这样做，因为Python 2和Qt4都已过时。

---

其他系统上的使用由于时间关系暂时未翻译：

### Raspberry Pi

### Fedora

### Gentoo

### openSUSE

### Arch Linux

### Older and non-conventional distributions



---

# Pivy

构建FreeCAD或启动FreeCAD不需要PIVY，但[Draft Workbench](https://wiki.freecadweb.org/Draft_Workbench)需要它作为运行时的依赖项。如果您不打算使用这个工作台，那么就不需要Pivy。然而，请注意Draft Workbench是由其他工作台在内部使用的，如[Arch](https://wiki.freecadweb.org/Arch_Workbench)和[BIM](https://wiki.freecadweb.org/BIM_Workbench)，因此需要安装Pivy来使用这些工作台。

到2015年11月，包含在FreeCAD源代码中的过时版本Pivy将不再在许多系统上编译。这不是一个大问题，因为通常你应该从发行版的包管理器中获取Pivy；如果您找不到Pivy，您可能不得不自己编译它，详情请参阅[Pivy编译说明](https://wiki.freecadweb.org/Extra_python_modules#Pivy)。

# Debug关键字

为了解决FreeCAD中的崩溃问题，Debug关键字在重要的依赖库(如Qt)的是很有用的，为此，请尝试安装以

`-dbg`、`-dbgsym`、`-debuginfo`或类似内容结尾的依赖包，这取决于您的Linux发行版。

对于Ubuntu，您可能需要启用特殊的存储库，以便能够使用包管理器查看和安装这些调试包。有关更多信息，请参见[Debug关键字包](https://wiki.ubuntu.com/Debug_Symbol_Packages)。

占楼更新，鸣谢 凡 [https://bbs.deepin.org/post/244528](https://bbs.deepin.org/post/244528)

---

# 编译 FreeCAD

> 在Python 2和Qt4上编译不再得到很好的支持，从0.20版本起根本不再得到支持。你应该编译Python 3和Qt5。   0.20版本至少需要Python3.6和Qt 5.9。

FreeCAD使用CMake作为它的主要构建系统，因为它可以在所有主要的操作系统上使用。用CMake编译通常非常简单，分为两个步骤。

1. CMake检查系统中是否存在每个所需的程序和库，并生成为第二步配置的 `Makefile`。FreeCAD有几个配置选项可供选择，但它提供了合理的默认值。下面详细介绍了一些备选方案。
2. 编译它，它由程序 `make`完成，生成FreeCAD可执行文件。

由于FreeCAD是一个大型应用程序，编译整个源代码可能需要10分钟到1小时不等，具体时间取决于您的CPU和用于编译的CPU核的数量。

您可以在源目录中或源目录外构建代码。**源外构建**通常是最好的选择。

**源外构建**

在单独的文件夹中构建比在源代码所在的同一个目录中构建更方便，因为每次更新源代码时，CMake可以智能地确定哪些文件已经更改，只重新编译需要的文件。这在测试不同的Git分支时非常有用，因为您不会混淆构建系统。

要进行源代码外构建，只需创建一个构建目录 `freecad-build`，区别于您的FreeCAD源文件夹 `freecad-source`；然后从这个构建目录将 `cmake`指向正确的源文件夹。您也可以在下面的说明中使用 `cmake-gui`或 `ccmake`代替 `cmake`。一旦cmake完成了环境的配置，就使用 `make`启动实际的编译。

```
mkdir freecad-build
cd freecad-build
cmake ../freecad-source
make -j$(nproc --ignore=2)
```

注意:如果你编译的是0.19版本分支，你必须显式指定你编译的是Qt5和Python 3——将上面的cMake命令替换为:

```
cmake ../freecad-source -DBUILD_QT5=ON -DPYTHON_EXECUTABLE=/usr/bin/python3
```

`make`的 `-j`选项控制并行编译多少程序(文件)。

`nproc`打印系统中的CPU核数，通过将它与 `-j`选项一起使用，您可以选择处理有多少核就处理多少文件，以加快程序的整体编译速度。

在上面的例子中，它将使用系统中的所有核心*，除了两个*；

当编译在后台进行时，这将使您的计算机对其他使用保持响应。FreeCAD可执行文件最终将出现在 `freecad-build/bin`目录中。参见[编译(加速)](https://wiki.freecadweb.org/Compiling_(Speeding_up))以提高编译速度。

**解决cmake问题**

如果你以前做过源代码外构建，并且被一个无法识别或似乎无法解决的依赖项卡住，请尝试以下方法:

* 在再次运行cmake之前，删除**build**目录的内容。FreeCAD是一个快速移动的目标，您可能会被缓存的cmake信息卡主，这些信息指向的是新存储库头无法使用的旧版本。清除缓存可以允许cmake恢复并识别实际需要的版本。
* 如果cmake提示丢失了一个特定的文件，请使用“`apt-file search`”之类的命令行，或其他包系统中的等效工具，来发现该文件属于什么包并安装它。请记住，您可能需要包的**-dev**版本，它携带FreeCAD使用该包所需的头文件或配置文件。

**编译GNU libc 2.34及更高版本**
GNU libc 2.34对库进行了更改，可能导致在某些Linux系统上的构建失败，出现像如下的错误:

`No rule to make target '/usr/lib/x86_64-linux-gnu/libdl.so`

要解决这个问题，必须从系统安装的**libdl.so.***(现在是空的)手动创建一个符号链接到一个位置（编译器提示它正在查找文件的位置）

例如（如果你的系统上实际安装的**libdl.so**副本是**/usr/lib/x86_64-linux-gnu/libdl.so.2**）：

```
sudo ln -s /usr/lib/x86_64-linux-gnu/libdl.so.2 /usr/lib/x86_64-linux-gnu/libdl.so
```

通过搜索**libdl.so***并将其链接到适当的位置，使该命令适合您的系统结构。

**源内构建**
如果您想快速编译一个版本的FreeCAD，并且不打算经常更新源代码，那么源内代码构建是很好的选择。在这种情况下，您可以通过删除单个文件夹来删除已编译的程序和源代码。

切换到源目录，并将 `cmake`指向当前目录(由一个点符号表示):

```
cd freecad-source
cmake . -DBUILD_QT5=ON -DPYTHON_EXECUTABLE=/usr/bin/python3
make -j$(nproc --ignore=2)
```

然后FreeCAD可执行文件将驻留在 `freecad-source/bin`目录中。

**如何修复您的源代码目录**
如果您不小心在源代码目录中执行了编译，或者添加了奇怪的文件，并且希望只将内容恢复到原始源代码，您可以执行以下步骤。

```
> .gitignore
git clean -df
git reset --hard HEAD
```

第一行清除 `.gitignore`文件。这确保了下面的**clean**和**reset**命令将影响目录中的所有内容，而不会忽略与 `.gitignore`中的表达式匹配的项。
第二行删除所有未被git存储库跟踪的文件和目录；
最后一个命令将重置对跟踪文件的任何更改，包括*第一个*清除 `.gitignore`文件的命令。
如果不清除源目录，如果代码发生更改，后续运行的 `cmake`可能不会捕获到系统的新选项。

**配置**
通过向cmake传递不同的选项，您可以改变FreeCAD的编译方式。语法如下所示。

```
cmake -D <var>:<type>=<value> $SOURCE_DIR
```

其中 `$SOURCE_DIR`是包含源代码的目录。`<type>`在大多数情况下可以省略。选项 `-D`后面的空格也可以省略。

例如，为了避免构建[FEM Workbench](https://wiki.freecadweb.org/FEM_Workbench):

```
cmake -D BUILD_FEM:BOOL=OFF ../freecad-source
cmake -DBUILD_FEM=OFF ../freecad-source
```

所有可能的变量都列在位于 `cMake/FreeCAD_Helpers`目录下的 `InitializeFreeCADBuildOptions.cmake`文件中。在这个文件中，搜索单词 `option`以获得可以设置的变量，并查看它们的默认值。

```
# ==============================================================================
# =================   All the options for the build process    =================
# ==============================================================================

option(BUILD_FORCE_DIRECTORY "The build directory must be different to the source directory." OFF)
option(BUILD_GUI "Build FreeCAD Gui. Otherwise you have only the command line and the Python import module." ON)
option(FREECAD_USE_EXTERNAL_ZIPIOS "Use system installed zipios++ instead of the bundled." OFF)
option(FREECAD_USE_EXTERNAL_SMESH "Use system installed smesh instead of the bundled." OFF)
...
```

又或者，使用命令 `cmake -LH`列出当前配置，从而列出所有可以更改的变量。您也可以安装并使用 `cmake-gui`来启动一个显示所有可以被修改的变量的图形界面。在下一节中，我们将列出您可能想要使用的一些更相关的选项。

**Debug版本构建**

创建一个 `Debug`版本来排除FreeCAD中的崩溃故障。注意，在这种构建下，[Sketcher](https://wiki.freecadweb.org/Sketcher_Workbench)对于复杂的草图会变得非常慢。

```
cmake -DBUILD_QT5=ON -DPYTHON_EXECUTABLE=/usr/bin/python3 -DCMAKE_BUILD_TYPE=Debug ../freecad-source
```

**Release版本构建**

创建一个 `Release`版本来测试代码不会崩溃。`Release`版本将比 `Debug`版本运行得更快。

```
cmake -DBUILD_QT5=ON -DPYTHON_EXECUTABLE=/usr/bin/python3 -DCMAKE_BUILD_TYPE=Release ../freecad-source
```

**针对Python 3和Qt5构建**

默认情况下，针对Python 2和Qt4的FreeCAD 0.19和更早版本。由于这两个包已经过时，所以最好为Python 3和Qt5构建。在FreeCAD 0.20中已经删除了对Python 2和Qt4的支持，如果编译最新的开发版本，则不需要显式启用Qt5和Python 3。

在现代Linux发行版中，您只需要提供两个变量来指定Qt5的使用，以及Python解释器的路径即可。

在0.19版本中:

```
cmake -DBUILD_QT5=ON -DPYTHON_EXECUTABLE=/usr/bin/python3 ../freecad-source
```

在0.20_dev版本中:

```
cmake ../freecad-source
```

**注意，当在0.19和0.20版本之间切换时，可能需要在运行cmake之前删除CMakeCache.txt。**

**为特定的Python版本构建**

如果系统中默认的 `python`可执行文件是链接到python 2，`cmake`将尝试为该版本配置FreeCAD。你可以通过给出特定可执行文件的路径来选择另一个版本的Python:

```
cmake -DPYTHON_EXECUTABLE=/usr/bin/python3 ../freecad-source
```

如果这不起作用，你可能必须定义额外的变量，指向所需的Python库和目录：

```
cmake -DPYTHON_EXECUTABLE=/usr/bin/python3.6 \
    -DPYTHON_INCLUDE_DIR=/usr/include/python3.6m \
    -DPYTHON_LIBRARY=/usr/lib/x86_64-linux-gnu/libpython3.6m.so \
    -DPYTHON_PACKAGES_PATH=/usr/lib/python3.6/site-packages/ \
    ../freecad-source
```

同一个系统中可能有多个独立的Python版本，因此Python文件的位置和版本号将取决于特定的Linux发行版。使用 `python3 -V`显示当前使用的Python版本;只有前两个数字是必要的;例如，如果结果是 `Python 3.6.8`，则需要指定与3.6版本相关的目录。如果您不知道正确的目录，请尝试使用 `locate`命令搜索它们。

```
locate python3.6
```

您可以在终端中使用 `python3 -m site`来确定Debian系统上的 `site-packages`目录或 `dist-packages`包路径。

FreeCAD的一些组件(如PySide)试图自动检测系统上安装的最新Python版本，如果它与上面输入的不一致，则可能失败。添加以下cMake选项可能会解决这个问题:

```
-DPython3_FIND_STRATEGY=LOCATION
```

**用Qt Creator针对Python 3和Qt5版本的构建**

1. 启动Qt Creator
2. 点击**Open Project**（打开项目）
3. 导航到源代码所在的目录 `freecad-source/`，并选择最上面的 `CMakeLists.txt`文件。
4. 通过选择该文件，它将自动在上面运行 `cmake`，但如果没有正确设置适当的选项，它可能会失败。
5. 然后**Projects → Build & Run → Imported Kit → Build → Build Settings → CMake** （**项目-构建&运行-导入Kit配套工具-构建-构建设置-CMake）**。设置适当的构建目录 `freecad-build/`。
6. 在键值对话框中设置适当的变量，类型为 `String`和 `Bool`。
   
   ```
   PYTHON_EXECUTABLE=/usr/bin/python3
   BUILD_QT5=ON
   ```
7. 如果变量没有正确地加载项目，您可能必须去**Projects → Manage Kits → Kits → Default (or Imported Kit or similar) → CMake** 去配置（**项目→管理套件→套件→默认(或导入套件及相关)→CMake**）。然后按 `Change`，并按上面所述添加适当的配置。如果找不到系统Python，可能需要添加更多关于Python路径的变量。
   
   ```
   PYTHON_EXECUTABLE:STRING=/usr/bin/python3.7
   PYTHON_INCLUDE_DIR:STRING=/usr/include/python3.7m
   PYTHON_LIBRARY:STRING=/usr/lib/x86_64-linux-gnu/libpython3.7m.so
   PYTHON_PACKAGES_PATH:STRING=/usr/lib/python3.7/site-packages
   BUILD_QT5:BOOL=ON
   ```
   
   7.1 点击 `Apply（应用）`, 接着点击 `OK（确定）`.
   
   7.2 确保其他选项设置正确，例如，**Qt的版本**应该是当前安装在系统中的版本，如 `PATH (qt5)中的Qt 5.9.5`。
   
   点击 `Apply（应用）`, 接着点击 `OK（确定）`关闭配置。
   
   `cmake`程序应该再次自动运行，它应该用所有可以配置的变量填充整个键值对话框。
8. 然后**Projects → Build & Run → Imported Kit →Run → Run Settings → Run → Run Configuration**并选择 `FreeCADMain`来编译FreeCAD的图形版本，或者用 `FreeCADMainCMD`来编译FreeCAD的命令行版本。
9. 最后，去到菜单**Build → Build Project "FreeCAD"**。如果这是一个新的编译，它应该需要几分钟，包括几个小时，这取决于您可用的处理器的数量。

**Qt designer插件**

如果你想为FreeCAD开发Qt代码，你需要Qt Designer插件，它提供了FreeCAD的所有自定义小部件。

进入一个源代码的辅助目录，然后使用指定的项目文件运行 `qmake`来创建 `Makefile`；然后运行 `make`来编译插件。

```
cd freecad-source/src/Tools/plugins/widget
qmake plugin.pro
make
```

如果正在为Qt5编译，请确保 `qmake`二进制文件是该版本的二进制文件，以便生成的 `Makefile`包含Qt5所需的信息。

```
cd freecad-source/src/Tools/plugins/widget
$QT_DIR/bin/qmake plugin.pro
make
```

其中 `$QT_DIR`是存放Qt二进制库的目录，例如 `/usr/lib/x86_64-linux-gnu/qt5`。

创建的库是 `libFreeCAD_widgets.so`，需要将其复制到 `$QT_DIR/plugins/designer`。

```
sudo cp libFreeCAD_widgets.so $QT_DIR/plugins/designer
```

**外部或内部Pivy**
以前，Pivy的一个版本包含在FreeCAD的源代码中(内部的)。如果希望使用系统的Pivy副本(外部)，则需要使用 `-DFREECAD_USE_EXTERNAL_PIVY=1`。

在FreeCAD 0.16的开发过程中，使用外部Pivy成为默认选项，因此这个选项不再需要手动设置。

**Doxygen文档**
如果安装了Doxygen，就可以构建源代码文档。有关说明，请参阅[源代码文档](https://wiki.freecadweb.org/Source_documentation)。

## 附加的文档

FreeCAD的源代码非常广泛，使用CMake可以配置许多选项。充分学习使用CMake可能有助于为您的特定需求选择正确的选项。

* [CMake参考文档](https://cmake.org/documentation/)（Kitware编）。
* [如何构建一个基于CMake的项目](https://preshing.com/20170511/how-to-build-a-cmake-based-project/)(blog)-Preshing on programming。
* [学习CMake的脚本语言在15分钟](https://preshing.com/20170522/learn-cmakes-scripting-language-in-15-minutes/)(blog)-Preshing on programming。

## **制作一个debian软件包**

如果你计划从源代码中构建一个Debian包，你需要先安装某些包:

```
sudo apt install dh-make devscripts lintian
```

去到FreeCAD目录并输入

```
debuild
```

一旦构建了包，您可以使用 `lintian`来检查包是否包含错误

```
lintian freecad-package.deb
```

**带有checkinstall的 *.deb包**

Debian脚本 `checkinstall`允许创建一个*.deb包，可以使用标准的 `dpkg`命令进行安装和删除。它可能需要先被安装(在Ubuntu上使用 `sudo apt install checkinstall`)。它是交互式的，并且请求为所需信息提供有用的默认值。在此过程中，包会被安装并创建*.deb文件和备份存档。

为包定义一个名称和一个简短的描述是个不错的选择。

必须输入名称才能再次卸载它，描述将会被用 `dpkg -l`列出。默认名称“build”提供的信息并不是很多。

例子：

```
cd freecad-source/freecad-build
cmake ..
make
sudo checkinstall                                  # e.g. name=freecad-test1
```

结果是一个*.deb文件在freecad-build文件夹。默认情况下，Checkinstall将安装构建。以下是安装或卸载它的方法:

```
cd freecad-source/freecad-build
 ls |grep freecad
        freecad-test1_20220814-1_amd64.deb
 sudo dpkg -i freecad-test1_20220814-1_amd64.deb   # install
 dkpg -l |grep freecad                             # find by name
 sudo dpkg -r freecad-test1                        # uninstall by name
```

# 更新源代码

CMake系统允许您智能地更新源代码，并且只重新编译已更改的部分，从而使后续编译更快。

移动到FreeCAD源代码第一次下载的位置，并 `pull`新代码:

```
cd freecad-source
git pull
```

然后移动到最初编译代码的构建目录，并运行 `cmake`，指定当前目录(用圆点表示);然后用 `make`触发重新编译。

```
cd ../freecad-build
cmake .
make -j$(nproc --ignore=2)
```

# 卸载源代码

如果编译的源代码是用 `sudo make install`安装的(对于Debian系统来说)，文件会被复制到  **/usr/local** 文件夹中的几个子文件夹中。可以使用**install_manifest.txt**文件进行卸载。它已在编译期间创建到   build 文件夹中，并包含所有已安装的文件。只要这个文件存在，就可以卸载。

```
cd freecad-source/freecad-build
xargs sudo rm < install_manifest.txt
```

# 故障排除

**64位系统**

在为64位构建FreeCAD时，OpenCASCADE (OCCT) 64位包存在一个已知的问题。为了让FreeCAD正常运行，你可能需要运行 `configure`脚本并设置额外的 `CXXFLAGS`:

```
./configure CXXFLAGS="-D_OCC64"
```

对于基于Debian的系统，在使用预构建的OpenCASCADE包时不需要这个选项，因为这些包在内部设置了适当的 `CXXFLAGS`。

# **自动化构建脚本**

这是一个完整的FreeCAD构建所需要的所有内容。这是一种单脚本方法，适用于新安装的Linux发行版。这些命令将要求安装包和新的在线存储库的root密码。这些脚本应该运行在32位和64位版本上。它们针对不同的版本编写，但也可能运行在有或没有重大更改的更高版本上。

如果您的首选发行版有这样的脚本，请在FreeCAD论坛上讨论，以便我们可以合并它。

### Ubuntu

### openSUSE

### Debian Squeeze

```
# get the needed tools and libs
sudo apt-get install build-essential python libcoin60-dev libsoqt4-dev \
libxerces-c2-dev libboost-dev libboost-date-time-dev libboost-filesystem-dev \
libboost-graph-dev libboost-iostreams-dev libboost-program-options-dev \
libboost-serialization-dev libboost-signals-dev libboost-regex-dev \
libqt4-dev qt4-dev-tools python2.5-dev \
libsimage-dev libopencascade-dev \
libsoqt4-dev libode-dev subversion cmake libeigen2-dev python-pivy \
libtool autotools-dev automake gfortran
 
# checkout the latest source
git clone https://github.com/FreeCAD/FreeCAD.git freecad
 
# go to source dir
cd freecad
 
# build configuration 
cmake .
 
# build FreeCAD
# Note: to speed up build use all CPU cores: make -j$(nproc)
make
 
# test FreeCAD
cd bin
./FreeCAD -t 0
```

### Fedora 27/28/29

### Arch using AUR

FreeCAD的文档手册：[https://freecad.github.io/SourceDoc/annotated.html](https://freecad.github.io/SourceDoc/annotated.html)
