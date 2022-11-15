# Matplotlib 科研绘图方法

## 前言

科研工作者在进行汇报或发表论文时需要绘制大量图像，其绘制图像常常与实验数据相关，一个能够重复绘制、批量绘制的方法将极大优化绘图流程。可编程的绘图流程能够给予科研工作者极大的自由度和极高的效率。

部分期刊投稿要求提供可编辑的矢量图像。

Matplotlib是Python的可视化图形库，在功能与实现上与MATLAB的Plot相似，因此常用于科研绘图，能够简便的绘制统计、函数、云图等信息。

Matplotlib通常基于Numpy（矩阵）数据绘制图像，绘图时应考虑其适用范围：

- 如果绘制基于Pandas的数据，推荐使用Seaborn，其也是Python库而且是基于Matplotlib的集成库

- 如果要绘制流程图等示意图不推荐用Matplotlib

### 给Python初学者

Python是一门开源编程语言，其作为现代高级语言提供了非常容易理解和易于编写的语法，其提供了基于库的代码复用方法帮助用户快速编写程序。

让Python完成工作不仅需要学习其本身的语法，熟悉Python各种库的使用也是有必要的。

本项目后续所要介绍的Matplotlib是Python众多库之一。同样Numpy、Pandas皆为其中的库。其中Numpy几乎是Python所有数学库的基础，其提供了类似MATLAB的矩阵方法（这并不意味着你数据格式必须组成矩阵，向量，列表，数值都是可以接受的）。Pandas提供了类似Excel表格的方法，方便你管理包含不同类型数据的数据库。

大多数库是非Python官方的开发者所编写，这也是开源的意义。但Python本身也提供了不少的基础库方便用户编写高级的脚本。比如os库提供了方便的系统文件管理方法，如`os.listdir(path)`能够列出path路径下的所有文件。

全面学习各种库的方法是阅读库的官方文档（不是Python官方的文档），但Python也提供了一些帮助代码，如`help(function)`能够返回函数`function`的帮助，首先注意不是`help(function())`后者返回`function`函数的返回值（如果能运行的话）的帮助而不是函数本身的帮助；其次该帮助或程序自动生成开发者编写半自动生成，并不全面，详细信息仍需要看文档。还有一种常用的帮助方法是`dir(object)`，能够返回对象`object`的所有方法（方法使用像`object.function1()`这样，具体查阅Python的面向对象教程；Python的思想是“所有值都是对象”的，所以你可以对Python里几乎任何东西使用这种方法）

### 推荐使用Jupyter

Python社区提供了大量的Python编写运行方案，Jupyter是基于IPython的,IPython是基于Python的，其添加的特性是依次继承的。我只粗略的了解其关系，好在我们只需要知道它们运行的都是Python，完全按照Python的语法编写就行，这里也只对介绍其表象不介绍具体内核。

简单的说IPython是一个运行Python的程序。通常编程需要你当代码整体运行，IPython让你能够一步步运行代码。在使用Matplotlib时能够在运行完一段后自动绘制相应的图像。

Jupyter进一步将你的脚本分成几块，你可以任意运行它们，按照任意的顺序运行，或者反复运行一块代码，总之你可以在任意的时间运行任意的代码块。代码报错了也不用担心，修改报错的块后仍可以继续运行，或者反复修改并运行一块。其服务于“写一块运行一块”，非常适用与试验你的想法。

它们除了独立安装也被集成在Anaconda中，你可以通过安装Anaconda安装它们。

Jupyter 有Jupter Notebook和升级后的Jupyter Lab，建议搜索相应的教程学习它们。

# Matplotlib 基础

Matplotlib官网：https://matplotlib.org/

官网下的：

安装教程：https://matplotlib.org/stable/users/getting_started/

示例（便于查找各种有用的信息）：https://matplotlib.org/stable/gallery/index.html



在使用之前确认安装Python和Matplotlib，然后开始编写脚本。

首先需要导入`matplotlib.pyplot`简写为`plt`，plt是常用的模块，是画图的基础模块，有的功能可能需要导入其他的模块，具体参照官方示例。

```Pyt
import matplotlib.pyplot as plt
```

导入之后有两种方法开始画图：

```python
plt.plot([1,2,3,4],[1,4,2,3]) # 画一些数据
```

或

```py
fig, ax = plt.subplots()  # 创建一个轴容器
ax.plot([1, 2, 3, 4], [1, 4, 2, 3]);  # 在轴上画一些数据
```

如果没有`IPython`需要使用命令显示图片

```py
plt.show() # 显示图片（不管用ax还是plt，这里都使用plt）
```

![plot](D:\PythonStore\matplotlib科研绘图方法\Image\plot.png)

## plt还是ax

这两种方法的结果是一样的。`plot`是绘制一条折线，这里输入的两个列表分别是xy坐标。可以注意到其区别是一个前面是`plt`一个是`ax`，这之后统称`plt方法`和`ax方法`（此处代码里的`ax`是变量名，可以是任意合法名称，但其本质是`plt.subplots()`返回的`matplotlib.axes.Axes`对象；所以此处`ax`指的其实是`Axes`对象，不仅仅是变量名）

它们本质上是一样的，plt方法实际上是自动创建了一个ax。他们的区别在于此，ax方法需要手动创建容器，但用户可以自由的管理，比如一幅图里排列多个坐标轴；而plt方法只能在一张图里显示一个坐标轴，但其足够方便，你不需要管理Matplotlib的坐标轴系统。

如下列代码绘制一个带colorbar图像：

```python
import matplotlib.pyplot as plt
import numpy as np
# 生成数据
np.random.seed(0)
data = np.random.rand(25,25)
```

```python
plt.imshow(data)	# 显示图片（矩阵）
plt.colorbar() 		# 添加
```

```python
fig, ax = plt.subplots()# 创建轴
im = ax.imshow(data)	# 画图并用im接收所画对象
plt.colorbar(im)		# colorbar是一个单独的ax，这里使用plt自动创建，同时传递im对象，colorbar自动读取其中色阶信息
```

![colorbar](D:\PythonStore\matplotlib科研绘图方法\Image\colorbar.png)

它们绘图命令基本是一致的，但其修改方法略有不同，比如修改x轴的范围：

```python
ax.set_xlim(0,1) # ax修改x轴范围
```

```python
plt.xlim(0,1) # plt修改x轴范围
```

# 常见问题

## 中文显示

参考文章：https://zhuanlan.zhihu.com/p/501395717

## 图像保存



