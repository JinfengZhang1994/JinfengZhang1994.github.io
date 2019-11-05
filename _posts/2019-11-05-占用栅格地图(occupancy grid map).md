### 机器人地图分类
- 尺度地图(metric map)：每一个地点都可以用坐标来表示，比如经纬度。
- 拓扑地图(topological map)：每一个地点用一个点来表示，用边来连接相邻的点，即图论中的图。
- 语义地图(semantic map)：每一个地点和道路都会用标签的集合来表示。

### 占用栅格地图(occupancy grid map)
　　在通常的尺度地图中，对于一个点，要么有障碍物，要么没有障碍物。在占据栅格地图中，对于一个点，用p(s=1)来表示它是free状态的概率，用p(s=0)来表示它是occupied的状态的概率，两者的和为1。
  定义
  $$
  Odd(s)=\frac{p(s=1)}{p(s=0)}
  $$
  作为点的状态。当获得一个新的测量值$(Measurement,z~\{0,1\})$时，更新
  $$
  Odd(s|z)=\frac{p(s=1|z)}{p(s=0|z)}
  $$
  $Odd(s|z)$表示在$z$繁盛的条件下$s$的状态。
  根据贝叶斯公式，我们有:
  $$p(s=1|z)=\frac{p(z|s=1)p(s=1)}{p(z)}$$
  $$p(s=0|z)=\frac{p(z|s=0)p(s=0)}{p(z)}$$
  带入之后，得:
  $$Odd(s|z)=\frac{p(s=1|z)}{p(s=0|z)}=\frac{p(z|s=1)p(s=1)/p(z)}{p(z|s=0)p(s=0)/p(z)}=\frac{p(z|s=1)}{p(z|s=0)}Odd(s)$$
  两边取对数得：
  $$logOdds(s|z)=log\frac{p(z|s=1)}{p(z|s=1)}+logOdds(s)$$
  这样，含有测量值的项就只剩下了$log\frac{p(z|s=1)}{p(z|s=0)}$,称这个比值为测量值模型$(measurement\ model)$，标记为$lomeas$。测量值的模型只有两种：
  $$
  lofree = log\frac{p(z=0|s=1)}{p(z=0|s=0)}
  $$
  $$
  looccu = log\frac{p(z=1|s=1)}{p(z=1|s=0)}
  $$
  两者都是定值，这样，如果我们用$logOdd(s)$来表示位置$s$的状态$S$的话，我们的更新规则就进一步简化成了$S^+=S^-+lomeas$其中$S^+和S^-$分别表示测量值之后和之前$s$的状态。另外，在没有任何测量值的初始状态下，一个点的初始状态
  $$
  S_{init}=logOdd(s)=log\frac{p(s=1)}{p(s=0)}=log\frac{0.5}{0.5}=0
  $$
  经过这样的建模，更新一个点的状态就只需要做简单的加减法。
  假设我们设定$looccu=0.9,lofree=-0.7$。那么，一个点状态的数值越大，就表示越肯定它是$Occupied$状态，相反数值越小，就表示越肯定它是$free$的状态。上图展示了用两个激光传感器的数据更新地图的过程。在结果中，一个点颜色越深越肯定它是$free$的，颜色越浅越肯定它是$occupied$的。
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/2019110516443131.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3pqZjI1NDM3NzE5NjQ=,size_16,color_FFFFFF,t_70)
  转自:[https://zhuanlan.zhihu.com/p/21738718/]()
  
