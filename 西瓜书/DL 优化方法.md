# 神经网络优化算法

[视频地址](https://www.bilibili.com/video/av94067702)

[知乎地址](https://zhuanlan.zhihu.com/p/110104333)

[TOC]

### 基本框架：

> SGD→SGDM(加入指数加权平均思想)→AdaGrad(自动调节学习率)→RMSProp(Adagrad会累加之前所有的梯度平方，而RMSprop仅仅是计算对应的平均值，因此可缓解Adagrad算法学习率下降较快的问题。)→Adam

![截屏2020-03-08下午12.10.31](/Users/elvis/Desktop/截屏2020-03-08下午12.10.31.png)

#### 指数加权移动平均值：

$$
\begin{aligned}
v_{t} &=\beta v_{t-1}+(1-\beta) \theta_{t} =(1-\beta) \theta_{t}+\sum_{i=1}^{t-1}(1-\beta) \beta^{i} \theta_{t-i}
\end{aligned}
$$
$$\theta_{t-i}$$是 t-i 时刻观测值 

 通常对 权重$$\sum_{i=1}^{t-1}(1-\beta) \beta^{i}$$ 小于  $$\frac{1}{e}$$ 的观测值可以忽略不计  所以$$ \beta^{}$$ 通常 >= 0.9



### 只用了一阶动量：

#### **SGD with 动量：**


$$
\begin{array}{c}
\Delta \theta_{t}=-\eta \cdot \frac{m_{t}}{\sqrt{E}}=-\eta \cdot m_{t}=-\left(\beta m_{t-1}+\eta g_{t}\right) \\
\theta_{t+1}=\theta_{t}-\left(\beta m_{t-1}+\eta g_{t}\right)
\end{array}
$$

##### 该方法的优点：

避免了局部最优解 这样有可能可以继续优化下降

![截屏2020-03-09下午12.34.53](/Users/elvis/Library/Application Support/typora-user-images/截屏2020-03-09下午12.34.53.png)



#### **NAG(Nesterov Acculerated Gradient)：**

$$
\begin{array}{c}
\Delta \theta_{t}=-\eta \cdot \frac{m_{t}}{\sqrt{E}}=-\eta \cdot m_{t}=-\left(\beta m_{t-1}+\eta \nabla J\left(\theta_{t}-\beta m_{t-1}\right)\right) \\
\theta_{t+1}=\theta_{t}-\left(\beta m_{t-1}+\eta \nabla J\left(\theta_{t}-\beta m_{t-1}\right)\right)
\end{array}
$$

### 加入了二阶动量:

#### **AdaGrad:**

对不同维度的参数采用不同的学习率

对于那些更新幅度很大的参数，通常历史累计梯度的**平方和**会很大；相反地，对于那些更新幅度很小的参数，通常其历史累计梯度的**平方和**会很小。

##### 缺点：

Adagrad方法的主要缺点是，学习率η总是在降低和衰减。

因为每个附加项都是正的，在分母中累积了多个平方梯度值，故累积的总和在训练期间保持增长。这反过来又导致学习率下降，变为很小数量级的数字，该模型完全停止学习，停止获取新的额外知识。

####  **RMSProp/AdaDelta**：

加入了 指数加权移动平均值的思想  加入了窗口

####  Adam：

将`Momentum`和`RMSprop`结合起来形成的一种适用于不同深度学习结构的优化算法

