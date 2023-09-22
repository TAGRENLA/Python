[TOC]



# python解释器

## 什么是python解释器

就是安装目录中的`python.exe`文件，为python的核心组件！

![image-20230922180903627](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922180903627.png)

## 什么是虚拟环境解释器？

虚拟环境中的解释器通常都是基于全局解释器进行创建的。虚拟环境是通过复制全局Python解释器的文件和目录来创建的，然后在其中添加一些必要的文件和目录以实现隔离。

创建虚拟环境时，一个常见的做法是基于全局解释器的可执行文件（例如`python.exe`或`python3`）来创建一个新的解释器。这个新的解释器会被放置在虚拟环境的文件夹中，通常在虚拟环境的 `bin`（在Linux/macOS上）或 `Scripts`（在Windows上）目录中。这个解释器是虚拟环境的核心，用于运行虚拟环境中的Python代码。

虚拟环境中的解释器会继承全局解释器的版本和配置，但它是独立的，并且有自己的包安装目录。这允许你在虚拟环境中安装和管理项目特定的依赖，而不会影响全局Python环境，从而实现了环境隔离。

![image-20230922181440823](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922181440823.png)

![image-20230922181211753](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922181211753.png)



## 如何查看python解释器的位置？

| 系统    | 终端打开快捷键         | 终端查询命令   | 脚本查询       |
| ------- | ---------------------- | -------------- | -------------- |
| Windows | `Win + R`, 输入 `cmd`  | `where python` | Python脚本     |
| macOS   | `Command (⌘) + 空格`   | `which python` | Python脚本     |
| Linux   | `Ctrl + Alt + T`       | `which python` | Python脚本     |

`  Python脚本_win_mac_Lin`

`注意`：这个脚本会返回当`前脚本使用的python解释器`的位置，不一定是你的全局解释器，有可能是你的`虚拟`解释器！

~~~python
import sys
interpreter_path = sys.executable
print("当前脚本使用的Python解释器，不一定是全局解释器：", interpreter_path)
~~~

python脚本`返回全局解释器的路径`，里面的python.exe文件就是解释器

```python
import sys
global_interpreter = sys.base_exec_prefix
print("全局Python解释器的路径：", global_interpreter)
```

---

# 虚拟环境

##   什么是虚拟环境？virtual environment

虚拟环境（Virtual Environment），通常简称为虚拟环境，是一个独立的Python开发环境，与全局Python环境隔离开来(包括解释器都是分开的！但是虚拟环境的解释器是基于全局环境的解释器创建的！)。虚拟环境允许你在同一台计算机上创建和维护多个Python项目，每个项目都有自己的独立环境，包括Python解释器和项目特定的依赖包。



## 虚拟环境和全局环境的关系

虚拟环境（Virtual Environment）和全局环境（Global Environment）之间的关系是一种隔离和独立的关系。下面是它们之间的主要关系：

1. **独立性**：虚拟环境是一个独立的Python环境，它与全局Python环境相互隔离。这意味着在虚拟环境中安装的包和配置不会影响全局Python环境，反之亦然。
2. **隔离**：虚拟环境中包括了一个独立的Python解释器，以及与项目相关的依赖包。这些元素是在虚拟环境中创建的，不依赖于全局Python环境。这使得你可以在同一台计算机上同时管理多个项目，每个项目都有自己的虚拟环境，不会相互干扰。
3. **共享全局解释器**：虚拟环境通常是基于全局Python解释器创建的。这意味着它们使用了全局Python解释器的可执行文件，并继承了全局解释器的版本和配置。但虚拟环境中的解释器是独立的，不会受全局解释器的影响。
4. **项目隔离**：虚拟环境的主要目的是为了实现项目隔离。每个项目都可以有自己的虚拟环境，其中包含了项目所需的特定版本的Python解释器和依赖包。这使得项目可以独立开发、测试和部署，而不会受其他项目或全局环境的影响。

总的来说，虚拟环境提供了一种管理Python项目和依赖的方法，确保项目之间的隔离性和独立性。它们允许你在同一计算机上管理多个项目，每个项目都有自己的Python环境，而不会影响其他项目或全局环境。这对于开发和维护多个Python项目非常有用。

---

## 有了虚拟环境是否可以删除全局环境？

理论上是可以删除全局Python环境的，但是不建议删除全局Python环境，因为全局Python环境通常包含了系统所需的一些核心Python组件和库。删除全局环境可能导致系统不稳定，尤其是一些系统工具和应用程序可能依赖于全局Python环境。

---

## 如何创建虚拟环境——方法1？（想看就看看，不看也没关系，反正也不用）:joy:

创建虚拟环境通常需要使用Python的虚拟环境管理工具，其中最常用的是`venv`（在Python 3.3及更高版本中内置）和`virtualenv`。以下是使用这两种工具创建虚拟环境的步骤：

### 使用 `venv` 创建虚拟环境（Python 3.3及更高版本）：

1. 打开终端（命令提示符或终端窗口）。

2. 导航到你希望创建虚拟环境的目录。你可以使用`cd`命令来切换目录。

3. 运行以下命令来创建虚拟环境。将`myenv`替换为你喜欢的虚拟环境名称。

   ```
   bashCopy code
   python -m venv myenv
   ```

4. 等待命令完成。这将在当前目录中创建一个名为 `myenv` 的虚拟环境文件夹。

5. 要激活虚拟环境，请使用以下命令：

   - 在 Windows 上：

     ```
     bashCopy code
     myenv\Scripts\activate
     ```

   - 在 macOS 和 Linux 上：

     ```
     bashCopy code
     source myenv/bin/activate
     ```

   激活虚拟环境后，你将看到虚拟环境的名称出现在终端提示符前面，表示你已进入该环境。

### 使用 `virtualenv` 创建虚拟环境：

1. 安装 `virtualenv`：如果你还没有安装 `virtualenv`，你可以使用以下命令安装：

   ```
   bashCopy code
   pip install virtualenv
   ```

2. 打开终端，并导航到你希望创建虚拟环境的目录。

3. 运行以下命令来创建虚拟环境。将 `myenv` 替换为你喜欢的虚拟环境名称。

   ```
   bashCopy code
   virtualenv myenv
   ```

4. 等待命令完成。这将在当前目录中创建一个名为 `myenv` 的虚拟环境文件夹。

5. 要激活虚拟环境，请使用以下命令：

   - 在 Windows 上：

     ```
     bashCopy code
     myenv\Scripts\activate
     ```

   - 在 macOS 和 Linux 上：

     ```
     bashCopy code
     source myenv/bin/activate
     ```

   激活虚拟环境后，你将看到虚拟环境的名称出现在终端提示符前面，表示你已进入该环境。

无论你选择使用 `venv` 还是 `virtualenv`，创建虚拟环境都会隔离你的Python项目，允许你管理项目特定的依赖和环境配置。当你完成一个项目时，你可以轻松地退出虚拟环境并切换到其他项目。

## 如何创建虚拟环境——方法2（看这里超级常用）:astonished:

基于`pycharm`创建:

File-->New Project...

![image-20230922182143870](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922182143870.png)

![image-20230922182352595](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922182352595.png)

---

按着顺序看哈，这个`Location`是上面的第一个红框框！

![image-20230922182620367](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922182620367.png)

- `Location`(第一个框)：项目的存放地点！可以进行更改！

![image-20230922182742492](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922182742492.png)

- `Location`：虚拟环境的创建地址！核心文件！就是上面的这个文件夹！

  ![image-20230922182856745](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922182856745.png)

- `Base interpreter`:用来选择虚拟环境的基础解释器的。这个基础解释器是虚拟环境的基础，虚拟环境会在此基础上创建一个独立的Python环境，包括特定版本的Python解释器和依赖包。虚拟环境将复制基础解释器的一部分文件和配置，并在其基础上构建。这意味着虚拟环境中的Python解释器版本和配置会受到基础解释器的影响。

- `Inherit global site-packages`:如果`启用`该选项，虚拟环境将能够访问并使用`计算机上全局Python环境(全局范围也包括其他可能存在的虚拟环境)中已安装的包和库`。这意味着你可以在虚拟环境中使用全局环境中的Python包，而不必重复安装它们。

  存在以下问题，一般来讲不启用！

  1. **访问全局包**: 启用此选项允许你的虚拟环境使用全局Python环境中安装的包。这可以在不需要在虚拟环境中重新安装它们的情况下重复使用全局包。
  2. **潜在兼容性问题**: 使用全局包可能导致兼容性问题，特别是如果不同项目需要不同版本的相同包。你可能会意外使用全局环境中不与你的项目兼容的包的版本。
  3. **隔离性**: 虚拟环境的主要好处之一是隔离。当你继承全局 site-packages 时，部分地打破了这种隔离，因为你的虚拟环境可以与全局环境中的包互动。
  4. **依赖管理**: 如果你希望严格控制项目的依赖和版本，通常最好创建一个不继承全局 site-packages 的干净虚拟环境。这样，你可以为每个项目独立管理依赖关系。

- `Make available to all projects`:如果选择启用此选项，虚拟环境中安装的包和资源将被设置为全局可用。这意味着你可以在所有项目中访问和使用这些包和资源，而不需要在每个项目中都重新安装它们。

一般来讲两个`都不勾选`,形象点如下图：

![image-20230922184145769](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922184145769.png)

pycharm打招呼脚本，看各位心情自行勾选：

![image-20230922184321136](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922184321136.png)

脚本运行结果如下：

![image-20230922184442556](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922184442556.png)

---



# python包&模块

## 什么是模块

"模块"（Module）是一种组织和封装代码的方式。它是Python中的一个重要概念，用于将相关的函数、变量和语句组织在一起，以便更好地管理和重用代码

## 常规安装

简单安装安装较慢：

~~~cmd
pip install 模块名
~~~

安装的位置。通常直接在cmd中运行此命令会将指定的模块安装到，全局的python中去。

1. **指定Python版本**：

   你可以使用 `-V` 或 `--python` 选项来指定安装模块时要使用的Python版本。例如，如果你要安装在Python 3.8上，可以运行以下命令：

   ```
   bashCopy code
   pip install -V 3.8 模块名
   ```

2. **指定安装目录**：

   你可以使用 `-t` 或 `--target` 选项来指定安装模块的目录。例如，如果你希望将模块安装在特定目录 `/path/to/your/directory` 中，可以运行以下命令：

   ```
   bashCopy code
   pip install -t /path/to/your/directory 模块名
   ```

3. **指定镜像源**：

   如果你希望使用特定的镜像源来下载模块，可以使用 `-i` 或 `--index-url` 选项。例如，如果你要使用 https://pypi.org/simple 作为镜像源，可以运行以下命令：

   ```
   bashCopy code
   pip install -i https://pypi.org/simple 模块名
   ```

## 脚本批量安装！

其会安装到该脚本`使用的环境`中去，例如使用的是虚拟环境，就会安装到虚拟环境的包目录中去！

~~~python
import os

required_libraries = [
    'numpy', 'pandas', 'matplotlib', 'seaborn',  # 数据处理和可视化
    'scipy', 'statsmodels', 'scikit-learn', 'xgboost', 'lightgbm',  # 数据分析和机器学习
    'tensorflow', 'keras', 'pytorch', 'fastai',  # 深度学习框架
    'beautifulsoup4', 'requests', 'selenium',  # 网络数据获取和处理
    'jupyter', 'spyder', 'vscode',  # 开发环境
    'sqlalchemy', 'pymysql', 'psycopg2', 'sqlite',  # 数据库连接和操作
    'openpyxl', 'xlrd', 'xlwt', 'pandasql',  # Excel 和 SQL 数据操作
    'pyodbc', 'pandas-profiling', 'missingno',  # 数据质量分析和处理
    'plotly', 'dash', 'cufflinks',  # 交互式数据可视化
    'geopandas', 'folium',  # 地理数据分析和可视化
    'nltk', 'spaCy', 'gensim',  # 文本处理和自然语言处理
    'networkx', 'igraph',  # 图论和网络分析
    'statspy', 'pingouin',  # 统计分析
    'pandasgui', 'dtale',  # 数据分析 GUI 工具
    'auto_ml', 'tpot',  # 自动化机器学习
    'vaex', 'dask',  # 大数据集处理
    'yellowbrick', 'shap',  # 可视化模型解释
    'sympy', 'quantstats',  # 数学和金融分析
    'tabulate', 'pandas-flavor',  # 数据转换和操作
    'arrow', 'zope.interface',  # 日期和时间处理
    'cryptography', 'paramiko',  # 加密和远程连接
    'pkg_resources',
]

for i in required_libraries:
    code = f"pip install {i} -i https://pypi.tuna.tsinghua.edu.cn/simple"   # 可根据自己需求自行变更本行代码，本质就是cmd中输入的内容
    os.system('cmd /c "{}"'.format(code))
    print('\n')
    print(f'==================================')
    print(f'============{i}已经安装============')
    print(f'==================================')
    print('\n')

~~~

## 模块的安装位置

安装位置在对应环境的`lib/site-packages`文件夹中

- 虚拟环境：

  虚拟环境位置如：

  > D:\Users\python\venv\Lib\site-packages

  ![image-20230922185711547](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922185711547.png)



- 全局环境：

  全局环境位置如：

  > C:\Users\TAGRENLA\AppData\Local\Programs\Python\Python38\Lib\site-packages

  ![image-20230922185752820](https://tagrenla.oss-cn-beijing.aliyuncs.com/image-20230922185752820.png)

## 用脚本查看指定模块的安装位置

查看`指定模块`的安装位置

~~~python
import pkg_resources

def get_module_info(module_name):
    try:
        distribution = pkg_resources.get_distribution(module_name)
        version = distribution.version
        location = distribution.location
        return version, location
    except pkg_resources.DistributionNotFound:
        return None, None

module_name = input("请输入要查询的模块名: ")
version, location = get_module_info(module_name)
if version and location:
    print(f"模块 '{module_name}' 的版本是：{version}")
    print(f"模块 '{module_name}' 的位置是：{location}")
else:
    print(f"模块 '{module_name}' 未找到或未安装==或者未输入正确的模块名！")
~~~

查看当前脚本所在环境中的`全部脚本`的安装位置：

~~~python
import pkg_resources
from prettytable import PrettyTable

def get_module_location(module_name):
    try:
        distribution = pkg_resources.get_distribution(module_name)
        location = distribution.location
        return location
    except pkg_resources.DistributionNotFound:
        return "Not Found"

installed_packages = pkg_resources.working_set

table = PrettyTable(["Package", "Version", "Location"])

for package in installed_packages:
    package_name = package.key
    package_version = package.version
    package_location = get_module_location(package_name)
    table.add_row([package_name, package_version, package_location])

print(table)
~~~

## 查看当前python解释器中安装的所有的库

~~~python
import pkg_resources
from prettytable import PrettyTable

installed_packages = pkg_resources.working_set

table = PrettyTable(["Package", "Version"])

for package in installed_packages:
    table.add_row([package.key, package.version])

print(table)
~~~
上述代码会显示当前 Python 解释器所使用的环境中安装的所有库及其版本。这包括在当前虚拟环境或系统范围内安装的所有库。这将输出当前 Python 解释器所使用的环境中所有已安装的库的列表。如果你在特定的虚拟环境中运行这段代码，它将显示该虚拟环境中的库列表。如果你在全局环境中运行它，它将显示全局 Python 环境中的库列表。

<img src="https://img-blog.csdnimg.cn/32e2353116cd4ef68889259a98910c5b.png" alt="Image" width="500" height="400">















