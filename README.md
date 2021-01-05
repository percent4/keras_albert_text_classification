本项目采用Keras和ALBERT实现文本多分类任务，其中对ALBERT进行微调。

### 维护者

- jclian91

### 数据集

sougou小分类数据集，共有5个类别，分别为体育、健康、军事、教育、汽车。

划分为训练集和测试集，其中训练集每个分类800条样本，测试集每个分类100条样本。

### 代码结构

```
.
├── albert_tiny（albert tiny预训练模型）
│   ├── albert_config_tiny.json
│   ├── albert_model.ckpt.data-00000-of-00001
│   ├── albert_model.ckpt.index
│   ├── albert_model.ckpt.meta
│   ├── checkpoint
│   └── vocab.txt
├── albert_base_zh_additional_36k_steps（albert base预训练模型）
│   ├── albert_config_base.json
│   ├── albert_model.ckpt.data-00000-of-00001
│   ├── albert_model.ckpt.index
│   ├── albert_model.ckpt.meta
│   ├── checkpoint
│   └── vocab.txt
├── albert_xlarge_zh_183k（albert large预训练模型）
│   ├── albert_config_xlarge.json
│   ├── albert_model.ckpt.data-00000-of-00001
│   ├── albert_model.ckpt.index
│   ├── albert_model.ckpt.meta
│   ├── checkpoint
│   └── vocab.txt
├── albert.py（albert模型构建脚本，来自开源项目）
├── albert_test.py（albert模型导入测试脚本）
├── data（数据集）
│   └── sougou_mini
│       ├── test.csv
│       └── train.csv
├── label.json（标签词典）
├── model_evaluate.py（模型评估脚本）
├── model_predict.py（模型预测脚本）
├── model_train.py（模型训练脚本）
├── README.md
└── requirements.txt（第三方模块）
```

## 模型效果

- sougou数据集, albert-tiny

模型参数: batch_size = 8, maxlen = 300, epoch=3

评估结果:

```
                precision   recall    f1-score   support

          体育     0.9700    0.9798    0.9749        99
          健康     0.9278    0.9091    0.9184        99
          军事     0.9899    0.9899    0.9899        99
          教育     0.8585    0.9192    0.8878        99
          汽车     1.0000    0.9394    0.9688        99

    accuracy                         0.9475       495
   macro avg     0.9492    0.9475    0.9479       495
weighted avg     0.9492    0.9475    0.9479       495
```

- sougou数据集, albert_base_zh_additional_36k_steps

模型参数: batch_size = 8, maxlen = 300, epoch=3

评估结果:

```
              precision    recall  f1-score   support

          体育     0.9802    1.0000    0.9900        99
          健康     0.9684    0.9293    0.9485        99
          军事     1.0000    0.9899    0.9949        99
          教育     0.8739    0.9798    0.9238        99
          汽车     1.0000    0.9091    0.9524        99

    accuracy                         0.9616       495
   macro avg     0.9645    0.9616    0.9619       495
weighted avg     0.9645    0.9616    0.9619       495
```

- sougou数据集, albert_xlarge_zh_183k

模型参数: batch_size = 2, maxlen = 300, epoch=3

评估结果:

```
              precision    recall  f1-score   support

          体育     0.9898    0.9798    0.9848        99
          健康     0.9412    0.9697    0.9552        99
          军事     0.9706    1.0000    0.9851        99
          教育     0.9300    0.9394    0.9347        99
          汽车     0.9892    0.9293    0.9583        99

    accuracy                         0.9636       495
   macro avg     0.9642    0.9636    0.9636       495
weighted avg     0.9642    0.9636    0.9636       495
```

### 项目启动

1. 将ALBERT中文预训练模型放在对应的文件夹下
2. 所需Python第三方模块参考requirements.txt文档
3. 自己需要分类的数据按照data/sougou_mini的格式准备好
4. 调整模型参数，运行model_train.py进行模型训练
5. 运行model_evaluate.py进行模型评估
6. 运行model_predict.py对新文本进行评估