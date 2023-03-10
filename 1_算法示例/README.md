# 算法示例
## 使用指南
1. 按 CTRL + P 打开命令行面板，输入 terminal: Create New Terminal 打开一个命令行终端 或者按CTRL +直接打开命令行终端。
如果快捷键没有反应，请手动点击最下面那行状态栏的第四个图标，然后在弹出的tab里点击TERMINAL打开命令行终端。
2. 如果是在gitpod上运行本项目，会自动安装所需依赖包，手动安装方法如下： 在命令行里输入 `pip install -r requirements.txt` 按 ENTER 安装示例程序所需依赖库。
3. 在命令行里输入 `cd 1_算法示例` 并按 `ENTER` 进入"算法示例"目录。
4. 已经通过git lfs 上传模型文件至github上，gitpod无法访问，显示的是指针型文件，需要手动从github上下载放置于指定路径中或者将本项目克隆到本地运行。

> 如果是在gitpod上运行，按以下步骤操作：
> 下载预训练模型'1m-acc0.79ccks2019_rel.pth'放置于'1_算法示例/models/rel_cls/'下,下载链接：
> [https://github.com/case-smart-data-engineering/6.4.4-1/blob/main/1_%E7%AE%97%E6%B3%95%E7%A4%BA%E4%BE%8B/train/model/bert_pretrain/pytorch_model.bin]
> 如果是克隆到本地运行，按以下步骤操作：
> 直接把下载的pth文件复制粘贴于'1_算法示例/models/rel_cls/'下。

5. 对于数据部分，由于github的限制，以及对想要测试模型的读者，github的项目中存放的是原始数据集的切片，这样便于在线化运行。
如果有想要全部数据集的读者，可以从[https://pan.baidu.com/s/1XK3v6BQlnsvhGxgg-71IpA]下载json文件，密码'nlp0'，放置于`1_算法示例/data/`

6. 训练
Bert模型使用的是huggingface的Bert-base模型，命名实体部分的训练，直接运行mains/train_ner.py，关系抽取部分的训练，直接运行mains/train_rel.py

7. 测试
直接运行deploy/demo.py。会首先进行命名实体识别，然后将实体两两组成实体对进行关系分类。


## 项目说明
项目分两部分：
- 命名实体识别部分使用的是BiLSTM+CRF。
- 实体关系抽取使用的是Bert进行关系分类。

### 文件夹分类
- mains：NER和REL的训练器
- data_loader：存放的是数据处理器，完成对数据的预处理
- data：存放的是train、test和dev的数据集
- config_utils：存放的是NER和REL的网络模型参数
- models：保存的是NER和REL训练的checkpoint
- modules：保存的是NER和REL的网络结构
- deploy：项目的入口，demo会先运行实体识别，然后运行关系抽取。

tips:
1. 由于data文件夹中数据量很大，所以如果全部都使用，训练过程和验证、测试过程会变得很耗费时间，所以如果为了跑通模型，可以使用数据切片，减少数据量。

### 数据集说明
百度的DUIE数据集是业界规模最大的中文信息抽取数据集。它包含了43万三元组数据、21万中文句子。
句子的平均长度为54，每句话中的三元组数量的平均值为2.1。
下面是一个样本：
{"text": "据了解，《小姨多鹤》主要在大连和丹东大梨树影视城取景，是导演安建继《北风那个吹》之后拍摄的又一部极具东北文化气息的作品", 
  "spo_list": [{
  "predicate": "导演",
  "object_type": "人物",
  "subject_type": "影视作品",
  "object": "安建",
  "subject": "小姨多鹤"
  }, {
  "predicate": "导演",
  "object_type": "人物",
  "subject_type": "影视作品",
  "object": "安建",
  "subject": "北风那个吹"
  }]
}

- 数据集的下载
链接：https://pan.baidu.com/s/1XK3v6BQlnsvhGxgg-71IpA 
提取码：nlp0 

- 预训练模型和相关文件见
https://huggingface.co/bert-base-chinese/tree/main

## 运行结果
在训练完后会在`1_算法示例/models/`路径下保存训练结果，然后运行demo.py文件，会得到关系类别的预测结果

## 备注
如果是在命令行上运行代码，需要按照使用指南的顺序进入`正确的目录`才可运行成功。