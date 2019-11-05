#semantic 3d occupancy mapping through efficient high order crfs
***
转自:[https://zhuanlan.zhihu.com/p/43194432]()
传感器：stereo
3d建图：orb_slam
地图表达：grid
语义标签：CNN+CRF
数据集：KITTI
CRF函数：unary+pairwise+higher-order(超像素)
$$
E(x)=\sum_{i\in{\nu}}\psi_{i}(x_i)+\sum_{i,j\in{\nu}}\psi_{ij}(x_i,x_j)+\min_{y}(\sum_{c\in{S}}\psi_{c}(x_c,y_c)+\sum_{c,d\in{S}}\psi_{cd}(y_c,y_d))
$$
二元：
$$
\psi^{P}_{ij}(x_i,x_j)=\mu(x_i,x_j)\sum^{K}_{m=1}w^{(m)}k^{(m)}(f_i,f_j)
$$
$$
k(f_i,f_j)=w_1exp(-\frac{|p_i-p_j|}{2\theta^2_\alpha}-\frac{|I_i-I_j|}{2\theta^2_\beta})+w_2exp(-\frac{p_i-p_j}{2\theta^2_\gamma})
$$
高阶：
$$
\psi^{HO}_{c}(x_c)=\min_{y_c}\psi_c(x_c,y_c)=\min_{y_c}(\psi_c(y_c)+\sum_{i\in{c}}\psi_{ci}(y_c,x_i))
$$
$$
\psi_{ci}(y_c,x_i)=
\left \{
\begin{array}{b}
0\quad if\ y_c=x_i\\
k_c^l\quad Otherwise
\end{array}
\right.
$$
[公式编辑规则](https://www.jianshu.com/p/25f0139637b7)
## 1. geometric 3d mapping
- `3d mapping`:
- `color and label fusion`:For color fusion, we directly take the mean of different color observation in different views. For the label fusion, we follow the standard Bayes’ update rule similar to that in occupancy mapping
## 2. hierarchical semantic mapping(semantic 3d labelling)

## 3. occupancy grid map

