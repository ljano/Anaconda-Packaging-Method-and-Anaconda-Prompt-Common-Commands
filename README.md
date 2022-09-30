Anaconda装包方法 &amp; Anaconda Prompt常用命令 &amp; Anaconda一些问题记录
[TOC]

# Anaconda装包方法 & Anaconda Prompt常用命令

## 方法一  Anaconda Navigator

直接进入对应环境安装即可

> 进入navigator慢解决办法
>
> 1. 挂梯子
> 2. 断网（没试过）
> 3. 换电脑（亲测有效，嘎嘎快。也有可能是win11的原因）

## 方法二  Anaconda Prompt（better）

***一定要先切换到对应环境再执行以下操作***

> 切换环境方法：`activate <环境名>` （conda不用但需要指定）

- #### **一般方法**：`pip/conda install <包名>`

  > 1. ***conda***无法进行安装时，可以使用***pip***进行安装，若均不行则可前往http://Anaconda.org搜索包名安装
  >
  > 2. pip无法更新python，因为pip并不将python视为包
  > 3. pip只是包管理器，无法对环境进行管理，而conda可以

- #### **离线安装法（百分百成功）**：

**1. 到一个库包源的网站下载所需要的安装包**

> 例如：https://www.lfd.uci.edu/~gohlke/pythonlibs/
>
> ```
> `ctrl+f`检索自己需要的包
> 
> cp39表示python版本号为3.9.x，amd64为64位
> ```

**2. 去对应文件夹复制路径，再进入包所在文件夹**

> 进入盘符方法：`d:`，不必加`cd`，而进入文件夹需要加`cd`
>
> 返回上一级盘符：`cd ..`
>
> **进入指定路径方法**：
>
> 1. 先进入对应盘：`d:`
> 2. 再进入对应文件夹：`cd python\site-packages`

**3. `pip install <下载的轮子>`**



## 【附录一】Anaconda Prompt常用命令之***“管理环境”***

#### **1. 创建新环境**

```text
conda create --name <env_name> <package_names>
```

- 注意：

  1. ***--name*** 可简写为 ***-n***

  2. ***<env_name>***  ：创建的环境名。建议以英文命名，且不加空格。

  3. ***<package_names>***  ：安装在环境中的包名。

     > 指定python版本和安装多个包的方法示例：
     >
     > **`conda create -n python_hhh python=3.9.13 numpy pandas`**  :创建一个名为“python_hhh”的环境，环境中安装版本为3.9.13的python，同时也安装了numpy和pandas包

  4. 新创建的环境将会被保存在下载的***/anaconda/envs***目录下。

#### **2. 切换环境**

```text
activate <env_name>
```

- 注意

1. 若创建环境后没有指定Python的版本，那么将默认安装与Anaconda版本相同的Python版本。

2. 当成功切换环境之后，在该行行首将以“(env_name)”或“[env_name]”开头。

#### **3. 退出环境至root(base)**

```text
deactivate
```

#### **4. 显示已创建环境**

```text
1. conda info --envs
```

```text
2. conda info -e
```

```text
3. conda env list
```

#### **5. 复制环境**

```text
conda create --name <new_env_name> --clone <copied_env_name>
```

- 注意：克隆后环境中将同时存在“copied_env_name”和“new_env_name”环境，且两个环境的配置相同。

#### **6. 备份/恢复/移动环境**

1. 进入（激活）需要备份的环境：

```text
conda activate <env_name>
```

2. 生成环境文件：（环境文件的名字可以随便起）

```text
conda env export > <new_env_name>.yaml
```

3. 安装文件中的环境：（建议执行此操作时挂梯子，否则慢且可能报错）

```text
conda env create -f <new_env_name>.yaml
```

- 注意：

1. 安装的环境名称并不是环境文件名，而是写在<new_env_name>.yaml文件中第一行的**`name:`**后

2. 跨操作系统安装会报错，因为环境中有一些操作系统固有的包，无法安装到另一个操作系统上

3. 至第2步即备份成功，备份的yaml文件默认存储于**`C:\Users\Yeryo`**目录下，其中Yeryo为用户名。也可直接用everything全盘搜索。

4. 在本地执行第3步即为恢复环境，在另一台设备上即为移动环境。

5. 此外，也可直接在Anaconda Navigator图形界面采用Anaconda Nucleus账号进行备份转移：


   <image src = "https://user-images.githubusercontent.com/69563081/193240680-e897e5e3-a5d5-4b0d-ab20-a05b3f1a1148.png" width=300>
   <image src = "https://user-images.githubusercontent.com/69563081/193240733-bbed4cd2-c7ee-4d43-bf99-e683ec3be02d.png" width=500>

   选中需要备份的环境，点击backup即可。

   再在本地或另一台设备上点击import再按下图操作即可：

    <image src = "https://user-images.githubusercontent.com/69563081/193240766-92f5f461-1c1f-4137-bc5d-ba8c9d82c502.png" width=500>

   

#### **8. 删除环境**

```text
conda remove --name <env_name> --all
```



## 【附录二】Anaconda Prompt常用命令之***“管理包”***

#### **1. 获取当前环境中已安装的包信息**

```text
conda list
```

#### **2. 安装包**

**① 在指定环境中安装包**

```text
conda install --name <env_name> <package_name>
```

**② 在当前环境中安装包**

```text
1. conda install <package_name>
```

```text
2. pip install <package_name>
```

**④ 从http://Anaconda.org安装包**

当使用 ***conda install*** 无法进行安装时，可以考虑从[http://Anaconda.org](https://link.zhihu.com/?target=http%3A//Anaconda.org)中获取安装包的命令，并进行安装。直接搜索即可，无需注册

#### **3. 更新包**

> 命令可使用update或upgrade，下面仅展示update

**① 更新所有包**

```text
conda update --all
```

**② 更新指定包**

```text
conda update <package_name>
```

> 更新多个指定包，则包名以**空格**隔开，向后排列

#### **4. 卸载包**

**① 卸载指定环境中的包**

```text
conda remove --name <env_name> <package_name>
```

**② 卸载当前环境中的包**

```text
conda remove <package_name>
```

在虚拟环境中实际要使用如下命令卸载：

```
pip uninstall <package_name>
```

否则报错如下：

> PackagesNotFoundError: The following packages are missing from the target environment



## 【附录三】Anaconda Prompt常用命令之***“管理conda”***

#### **1. 验证conda已被安装**

```text
conda --version
```

#### **2. 更新conda至最新版本**

```text
conda update conda
```

#### **3. 查看conda帮助信息**

```text
conda -h
```

#### **4. 卸载conda**

```text
控制面板 → 添加或删除程序 → 选择“Python X.X (Anaconda)” → 点击“删除程序”(win10好像不太一样)
```



## 【附录四】Anaconda相关的一些问题

1. 安装anaconda时警告`...2 spaces...`

   - **原因：**是因为安装路径中存在空格，常见的是Program Files (x86)目录，有俩空格

   - **解决办法：**装在不含空格的目录即可

2. 在pycharm中配置anaconda时可能会报错如下：

   `Conda executable path is empty`

   - **原因：**见https://blog.csdn.net/qq_43750301/article/details/126937553。我的原因是直接进行了下图2的操作，未进行操作1.

   - **解决方法：**

   1. 先执行下图1处操作，选择anaconda自带的_conda.exe文件
   2. 再执行下图2处操作，选择anaconda3\envs中自己需要的环境的python.exe文件即可
    <image src = "https://user-images.githubusercontent.com/69563081/193240816-6179453f-394d-45db-901d-7d41fd2a919a.png" width=900>
