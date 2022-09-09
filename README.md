# vLoong能源AI挑战赛——异常检测赛参赛手册

# 一、活动背景

汽车产业正在经历巨大变革，新能源汽车市场规模持续扩大，电池安全问题日益引发重视。 电池异常检测面临着汽车数据质量差，检出率低，误报率高，大量无效报警无法直接自动化运维等弊端。

为了更好的检验电池安全问题，**比赛通过募集优秀异常检测方案，对实车数据进行特征提取、参数优化、异常对比等手段，优化异常检测结果，使更好的应用于车辆预警、故障模式识别等多种场景。**

# 二、赛程赛制

![img](https://github.com/thinkenergy/vloong-Anomaly-detection/blob/master/static/流程图.jpg)

## **2.1 整体说明**

1、**报名**:报名活动的同学，你可选择在飞桨社区报名或进入vLoong大赛官方社群进行报名，所有大赛相关信息都会在群中及时同步；

2、**赛题**:完成报名后，你可点击查看数据要求并下载数据，非飞桨社区参赛用户需并在GitHub内建立Repo存储自己的代码以方便提交；

3、**福利**:参赛选手可先跑通赛事组提供的参考算法进行实验，以便更好的理解赛题；跑通后可发邮件至[ vLoong@thinkenergy.tech ](http://vLoong@thinkenergy.tech)联系工作人员，邮件模板见[邮件提交规范](https://github.com/thinkenergy/vloong-Anomaly-detection/blob/master/邮件提交规范.md)，经邮件确认后可以分配 **专属导师** ，一对一贴身提供答疑指导；

4、**提升**:参赛选手需基于主办方提供的数据和赛题任务进行优化和实现，参赛者可在主办方提供的参考算法上持续调参优化或自由使用任意数据加工处理、特征提取、异常检出算法或工具；

5、**AUC**:参赛选手优化目标为AUC，最终按照核验后AUC排名确认奖项；

6、**提交**:本次比赛采用**AB榜**形式，**A榜**数据为“部分测试集”数据，选手可以多次提交刷分，A榜会定期更新以方便选手了解比赛进度。按照官方 [REPO 提交规范_异常检测](https://github.com/thinkenergy/vloong-Anomaly-detection/blob/master/REPO提交规范_异常检测.md)中的文档和规范，非飞桨参赛用户需发邮件至[ vLoong@thinkenergy.tech ](http://vLoong@thinkenergy.tech)提交作品，邮件模板见[邮件提交规范](https://github.com/thinkenergy/vloong-Anomaly-detection/blob/master/邮件提交规范.md)；**飞桨参赛用户可在飞桨社区内直接提交，提交时需把结果文件和代码同时提交**；

7、**评审**:组委会在全部提交完成后7个工作日内验证A榜选手AUC结果，验证中如需修改会及时与选手沟通，组委会验证后AUC排名会更新在**B榜**，B榜排名即为比赛最终成绩(**选手所用的数据为“训练集”和“部分测试集”，组委会核验使用的数据是“全量测试集”，最终核验后AUC值可能与选手提交结果不一致**)；

8、**发奖**:最终提交检测精度、代码规范、Repo文档、PR代码符合要求后，将公示最终比赛结果，**依据最终AUC排名瓜分万元现金大奖！**

## **2.2 数据下载**

| **数据集**                        | **参考代码**                                                 | 评价标准 |
| --------------------------------- | ------------------------------------------------------------ | -------- |
| https://share.weiyun.com/A8jkfKL8 | [template](https://github.com/thinkenergy/vloong-Anomaly-detection/tree/master/repo_template ) | AUC      |

## 2.3 时间安排

| **时间**         | **日程**              |
| ---------------- | --------------------- |
| 2022/9/14        | 发布比赛&报名入口开启 |
| 2022/10/15 24:00 | 报名入口关闭          |
| 2022/10/15 24:00 | 比赛结果截止提交      |
| 2022/10下旬      | 主办方线下验证（B榜） |

## **2.4 奖项设置**

| **奖项** | **个数（团队）** | **奖励** |
| -------- | ---------------- | -------- |
| 冠军奖   | 1                | ¥5000    |
| 亚军奖   | 2                | ¥2000    |
| 季军奖   | 3                | ¥500     |

**其他奖励**

比赛中表现优异的同学有机会获得**昇科能源实习绿色通道**和加入**vLoong Studio人才计划**机会。

> vLoong Studio是由昇科能源与欧阳明高院士工作站联合设立，旨在研发前沿AI for Smart Energy技术，探索AI技术在新能源领域的应用，促进学科交叉，实现AI技术产业化落地，培养高级电池AI人才。

**特别注意**:以上所有提及金额均为税前金额。

## **2.5 参赛方式**

### 2.5.1  参赛对象

本次竞赛面向全社会开放，不限年龄、身份、国籍，相关领域的个人、高等校、科研机构、企业单位、初创团队等人员均可报名参赛。

### 2.5.2  参赛要求

（1）支持以个人或团队（线下自由组队）的形式参赛，队伍人数最多不超过3人，**建议编程达人、数据挖掘爱好者、跨单位/院校组队参赛**,每人只能参加一支队伍。如果是多人团队，则需确认一名队长，负责沟通事宜。

（2）参赛选手报名须保证所提供的个人信息真实、准确、有效。如发放奖金或礼品时发现选手填写的报名信息与个人身份不相符，组委会将保留停止发放奖金或礼品的权利。

（3）大赛所提供的数据集和平台仅限于此次大赛使用，不得用于其他任何目的。若因违反此规定而给数据提供方或平台提供方造成损失的，参赛队伍所在单位和选手须承担全部责任；

（4）vLoong算力平台是昇科能源自主研发的 vGRU 深度学习框架，配备了可智能化调度的算力提供在线编程环境、免费GPU算力、海量开源算法和开放数据，帮助开发者快速创建和部署模型。

（5）参赛者同意授予举办方在全球范围内、无限期、不受限制的免费使用前款成果的权利，包括但不限于用于服务提供、进一步开发服务、用于商业用途及分许可他人使用。为免歧义，基于上述成果使用所产生的新成果，举办方享有完整的知识产权，参赛者同意对新成果不主张任何权益，包括但不限于所有权、以及基于对上述成果享有的所有权而阻碍新成果的实施等。

（6）官方交流报名群

![img](https://github.com/thinkenergy/vloong-Anomaly-detection/blob/master/static/异常检测海报.jpg)

### 2.5.3  vLoong系列挑战赛不收取任何报名费用。

## 2.6 反作弊声明

- 参与者禁止加入多个队伍报名，一经发现将取消成绩；

- 参与者禁止在指定考核技术能力的范围外利用规则漏洞或技术漏洞等不良途径提高成绩排名，一经发现取消成绩；

- 参与者如有恶意提交、抄袭等违规作弊的现象，可能会取消比赛资格。

## 2.7 其他

主办方有权根据赛事进展调整日期，修订规则；主办方在法律法规许可范围内对本比赛规程享有解释权。

# 三、主办方&合作方

vLoong智慧能源开放社区、北京昇科能源科技有限公司、欧阳明高院士工作站暨四川新能源汽车创新中心、百度飞桨