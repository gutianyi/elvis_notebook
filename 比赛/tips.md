- 特征工程具体流程：
  1. 对时间做处理  年月日
  2. 拿到特征列表
  3. 缺省值做填充
  4. 对类别型变量 one- hot encoding 
  5. 对连续值变量做 scaling
  6. 训练和分析





https://zhuanlan.zhihu.com/p/39729525

* 查看数据源 异常值

  1. zero值（describe()从min max中查询）

  2. 重复值 `listings['name'].duplicated().value_counts()`

  3. 期中有测试 nan  不能用的情况  str可以用下面方法

     `listings = listings.drop(listings[listings['name'].str.contains('测试|np.NaN|不能租|test|下架|下线',na = True)].index)`

  4. `listings = listings.drop_duplicates() ` 去除重复值



* pandas的替换和部分替换
  1. `df.replace(to_replace, value,inplace = True)`  替换全部
  2. `train_dataset.loc[train_dataset["Sex"] == "male",'Sex'] = 1`
  3. `train_dataset["Age"] = train_dataset['Age'].fillna(train_dataset['Age'].mean()) `填充NaN值



* 对于缺失值的处理方法

  对数据进行分析的时候要注意其中是否有缺失值。一些机器学习算法能够处理缺失值，比如神经网络，一些则不能。
  对于缺失值，一般有以下几种处理方法:

  1. 如果数据集很多，但有很少的缺失值，可以删掉带缺失值的行；
  2. 如果该属性相对学习来说不是很重要，可以对缺失值赋均值或者众数。（详细可见 异常值处理）
  3. 对于标称属性，可以赋一个代表缺失的值，比如‘U0’。因为缺失本身也可能代表着一些隐含信息。比如船舱号Cabin这一属性，缺失可能代表并没有船舱。
  4. 使用回归 随机森林等模型来预测缺失属性的值。因为Age在该数据集里是一个相当重要的特征（先对Age进行分析即可得知），所以保证一定的缺失值填充准确率是非常重要的，对结果也会产生较大影响。一般情况下，会使用数据完整的条目作为模型的训练集，以此来预测缺失值。对于当前的这个数据，可以使用随机森林来预测也可以使用线性回归预测。这里使用随机森林预测模型，选取数据集中的数值属性作为特征（因为sklearn的模型只能处理数值属性，所以这里先仅选取数值特征，但在实际的应用中需要将非数值特征转换为数值特征）

* 对df进行分析

  `DataFrame.describe(percentiles=None,include=None,exclude=None)`

  Eg: `df.describe(include=['O'])`  or `train_df.describe(include=np.object)`

