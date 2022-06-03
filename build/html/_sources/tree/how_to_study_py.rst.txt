大家好，前两天有粉丝问有关算法预测的问题。今天我们就以股价预测为例，分享一下两种预测方法：

-  常规方式股票预测
-  新方 #### 1. 常规方式股票预测

1.1 数据集介绍
==============

本文使用的股价数据集来自GitHib：\ ``https://github.com/pierpaolo28/Data-Visualization/blob/master/Dash/stock_data.csv``\ 。

下载数据集后，查看其内容，可以看到数据集中包含时间、开盘时股价等一系列相关信息，本文需要预测的是股价当天的最终价格，即
``Close`` 列的数据：

.. figure:: https://img-blog.csdnimg.cn/756f3d0021fd4957956e253a94763217.png#pic_center
   :alt: 股价数据集

   股价数据集

1.2 模型分析
============

为了预测股价，我们根据以下思路构建神经网络模型：

-  按照时间发生顺序对数据集进行排序
-  以前五个股票价格数据作为输入，第六个股票价格数据作为输出
-  滑动时间窗口，在模型的下一个输入使用第二个到第六个数据，并将第七个数据作为输出，依此类推，直到到达最后一个数据点
-  由于我们需要预测的是一个连续值，因此损失函数使用均方误差值
-  此外，我们还将在下个环节尝试利用文本数据集成到历史股票价格数据中，以预测第二天股价的情况

1.3 使用神经网络进行股价预测
============================

根据以上模型的思路，接下来，我们使用 ``Keras``
实现神经网络模型用于预测股价。

1.导入相关的包和数据集：

::

   import pandas as pd
   data2 = pd.read_csv('content/stock_data.csv')

2.按照前述分析准备数据集，其中输入是前五天的股票价格，输出是第六天的股票价格：

::

   x = []
   y = []
   for i in range(data2.shape[0]-5):
       x.append(data2.loc[i:(i+4)]['Close'].values)
       y.append(data2.loc[i+5]['Close'])

   import numpy as np
   x = np.array(x)
   y = np.array(y)

3.准备训练和测试数据集，构建模型：

::

   from sklearn.model_selection import train_test_split
   x_train, x_test, y_train, y_test = train_test_split(x, y, test_size=0.3)

   from keras.layers import Dense
   from keras.models import Sequential
   model = Sequential()

   model.add(Dense(100, input_dim=5, activation='relu'))
   model.add(Dense(1, activation='linear'))

4.建立模型并进行编译：

::

   model.compile(optimizer='adam', loss='mean_squared_error')
   model.summary()

看以看到，模型的简要信息输出如下：

::

   Model: "sequential"
   _________________________________________________________________
   Layer (type)                 Output Shape              Param 
   =================================================================
   dense (Dense)                (None, 100)               600       
   _________________________________________________________________
   dense_1 (Dense)              (None, 1)                 101       
   =================================================================
   Total params: 701
   Trainable params: 701
   Non-trainable params: 0
   _________________________________________________________________

可以看到，训练集股价的均方误差值约为
``320``\ ，而预测集股价的均方误差值约为
``330``\ ，以这种方式预测股价存在较大的问题。

在下一部分中，我们将学习如何在模型中将股价价格数据与新闻标题的文本数据集成在一起的方式进行预测。