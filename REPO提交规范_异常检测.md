# REPO 提交规范

项目和代码的规范和可读性对于项目开发至关重要，可以提升开发效率。本文给出开发者在新建开发者生态项目时的repo目录示例，以供参考。

本文示例项目在文件夹[repo_template](https://github.com/thinkenergy/vloong-Anomaly-detection/tree/master/repo_template)下，您可以将这个文件夹中的内容拷贝出去，放在自己的项目文件夹下，并编写对应的代码与文档。

注意： 该模板中仅给出了必要的代码结构，剩余部分，如模型组网、损失函数、数据处理等，与参考repo中的结构尽量保持一致，便于复现即可。

注意： 该repo中仅给出了使用notebook 的demo

## 1. 代码结构

- 方案一：可以提交notebook 文件，notebook 中写清楚各部分代码功能，包括数据处理、训练、模型保存、加载、提交文件生成等，适用于基于demo模型调参；

- 方案二：使用python 文件提交可以参考下面的目录结构，适用于基于demo模型调参或自行开发新模型；

- ​     建议的目录结构如下：

- - ```Plaintext
    ./repo_template               # 项目文件夹名称，可以修改为自己的文件夹名称
    |-- config                    # 配置类文件夹
    |   ├── competition.json      # 项目配置信息文件
    |-- dataset                   # 数据集类文件夹
    |   ├── dataset.py            # 数据集代码文件
    |-- log                       # 日志类文件夹
    |   ├── train.log             # 训练日志文件
    |-- model                     # 模型类文件夹
    |   ├── torch.model   # 训练好的模型文件
    |-- preprocess                # 预处理类文件夹
    |   ├── preprocess.py         # 数据预处理代码文件
    |-- tools                     # 工具类文件夹
    |   ├── train.py              # 训练代码文件
    |   ├── eval.py               # 验证代码文件
    |-- main.py                   # 项目主文件
    |-- README.md                 # 中文用户手册
    |-- LICENSE                   # LICENSE文件
    ```

  - config：项目配置类文件夹，包含项目配置信息等文件
  - dataset：数据集类文件夹，包含构建数据集等代码文件
  - log：日志类文件夹，包含训练日志等文件
  - model：模型类文件夹，包含训练好的模型文件
  - preprocess：预处理类文件夹，包含数据预处理等代码文件
  - tools： 工具类文件夹，包含训练、验证等代码文件
  - main.py：项目主文件，可进行项目全流程（训练+验证）执行过程
  - README.md： 中文版当前模型的使用说明，规范参考 README 内容要求
  - LICENSE： LICENSE文件

## 2. 功能实现

模型需要提供的功能包含：

- 训练：可以在GPU单机单卡的环境下执行训练

- 验证：可以在GPU单机单卡的环境下执行验证；可以实现模型和数据的加载，并用于推理，生成文件夹下各个充电片段的得分值

- 模型保存：保存已完成训练的模型，并且模型是可以根据参赛队伍提供的代码重新生成的，不能存在任何通过黑箱得到的模型，否则将认定为作弊行为

## 3. 命名规范和使用规范

- 文件和文件夹命名中，尽量使用下划线`_`代表空格，不要使用`-`。

- 模型定义过程中，需要有一个统一的变量（parameter）命名管理手段，如尽量手动声明每个变量的名字并支持名称可变，禁止将名称定义为一个常数（如"embedding"），避免在复用代码阶段出现各种诡异的问题。

- 重要文件，变量的名称定义过程中需要能够通过名字表明含义，禁止使用含混不清的名称，如net.py, aaa.py等。

- 在代码中定义path时，需要使用os.path.join完成，禁止使用string加的方式，导致模型对windows环境缺乏支持。

## 4. 注释和License

对于代码中重要的部分，需要加入注释介绍功能，帮助用户快速熟悉代码结构，包括但不仅限于：

- Dataset、DataLoader的定义。

- 整个模型定义，包括input，运算过程，loss等内容。

- init，save，load，等io部分

- 运行中间的关键状态，如print loss，save model等。

如：

```undefined
import pandas as pd
import torch

from torch.utils.data import Dataset


class BatteryDataset(Dataset):
    """
    Battery数据集定义
    """
    def __init__(self,data_path):
        """
        初始化
        :param data_path: 数据路径 str
        """
        super().__init__()
        self.install_data = pd.read_csv(data_path, encoding='utf8', sep=',') # 加载原始数据
        
    def __len__(self):
        """
        返回整个数据集大小
        """
        return len(self.install_data)
    
    def __getitem__(self, idx):
        """
        根据索引idx返回dataset[idx]
        :param idx: 数据索引 int
        """
        input_data = pd.DataFrame([])
        label = pd.DataFrame([])
        
        input_data = self.install_data.iloc[idx, 1] # 获取input数据
        label = self.install_data.iloc[idx, 0] # 获取数据集label
        return label, input_data
```

对于整个模型代码，都需要在文件头内加入licenses，readme中加入licenses标识。

文件头内LICENSE格式如下：

```Plaintext
# encoding=utf8
# Copyright (c) 2022 Circue Authors. All Rights Reserved

# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at

#     http://www.apache.org/licenses/LICENSE-2.0

# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.
```

## 5.数据集说明

本次比赛的数据集为经过处理的整车充电段数据，旨在借助充电数据分析车辆当前是否存在故障。

比赛选择了实际发生故障，但传统的报警系统没有起到预警作用的数据，希望众多优秀选手通过机器学习等方法，找到有效识别车辆故障的模型。

数据以pkl格式保存，每个pkl包含两部分数据。第一部分是车辆充电时的电压，电流等时序信息，共有8列数据，分别是['volt','current','soc','max_single_volt','min_single_volt','max_temp','min_temp','timestamp'],  对应的含义分别是[电压，电流，电池SOC，最大单体电压，最小单体电压，最高单体温度，最低单体温度，时间戳]。

充电段数据是新能源车辆电池数据中比较稳定的数据，电池的参数变化也更有规律，**需要注意数据已经过清洗，数值的大小不能再反应电池本身的特性**，但数据变化的趋势仍然符合电池的规律，下图是电压/电流/SOC在充电时随时间变化的示意图。

![img](https://github.com/thinkenergy/vloong-Anomaly-detection/blob/master/static/dMWk7REtfU.png)

pkl文件的第二部分是充电车辆的里程和标签，测试集没有标签

## 6. 评价指标

评价指标：AUC

AUC概念：AUC（area under curve)是一个模型的评价指标，用于分类任务，被定义为ROC曲线下与坐标轴围成的面积，取值范围在0.5和1之间。AUC越接近1.0，检测方法真实性越高;等于0.5时，则真实性最低，无应用价值。这个指标想表达的含义是随机抽出一对样本（一个正样本，一个负样本），然后用训练得到的分类器来对这两个样本进行预测，预测得到正样本的概率大于负样本概率的概率。

 AUC计算方法：通过直接统计预测label的逆序对数来实现，在有M个正样本，N个负样本的数据集里，一共有M*N对样本，统计这M*N对样本里，正样本的预测概率大于负样本预测概率的个数，计算公式如下：

![img](https://github.com/thinkenergy/vloong-Anomaly-detection/blob/master/static/formula-1.png)

 

![img](https://github.com/thinkenergy/vloong-Anomaly-detection/blob/master/static/formula-2.png)

## 7. 其他问题

- 代码封装得当，易读性好，不用一些随意的变量/类/函数命名

- 注释清晰，不仅说明做了什么，也要说明为什么这么做

- 随机控制，需要尽量固定含有随机因素模块的随机种子，保证模型可以正常复现

- 数据读取路径需写在项目配置信息文件competition.json中，并可进行调用。

## 8. README 内容&格式说明

模型的readme共分为以下几个部分，可以参考模板见：[README.md](https://github.com/thinkenergy/vloong-Anomaly-detection/blob/master/README_模板.md)

```Plaintext
# 模型名称
## 1. 简介
## 2. 数据集
## 3. 准备数据与环境
## 4. 开始使用
## 5. 代码结构与简要说明
## 6. LINENCE
## 7. 参考链接与文献
```

## 9. train.log 日志文件格式说明

参赛队伍若使用神经网络模型则需提供训练日志(train.log)文件，训练日志中需要包含当前的epoch和iter数量，当前loss、当前数据集精度

```undefined
from loguru import logger

logger.add("./train.log",
                   rotation="500MB",
                   encoding="utf-8",
                   enqueue=True,
                   retention="10 days")
                   
for i in range(100):    # 以总共训练100轮为例
    logger.info(f"epoch{i+1}/100:")
    logger.info("train_loss:")
    logger.info("train_mape:")
```