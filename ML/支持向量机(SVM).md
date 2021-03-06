## 支持向量机(SVM)

#### 1. 线性可分支持向量机

* 支持向量机最简单的情况就是线性可分支持向量机，或硬间隔支持向量机，条件是训练数据线性可分，学习策略是最大间隔法，可表示为凸二次规划问题。

  * 原始最优化问题为

    ![](D:\下载\CodeCogsEqn.gif)

    ![](D:\下载\CodeCogsEqn (1).gif)

    * 求得的最优化问题的解为`w*,b*`，得到线性可分支持向量机，分离超平面为

    ![](D:\下载\CodeCogsEqn (5).gif)

    ​	分类决策函数为

    ![](D:\下载\CodeCogsEqn (6).gif)

    * 线性可分支持向量机的最优解存在且唯一，位于间隔边界上的实例点为支持向量，最优分离超平面由支持向量完全决定。

  * 二次规划的对偶问题是

    ![](D:\下载\CodeCogsEqn (2).gif)

    ![](D:\下载\CodeCogsEqn (3).gif)

    ![](D:\下载\CodeCogsEqn (4).gif)

    * 通过求解对偶问题学习线性可分支持向量机，首先求得最优值`a*`,然后求最优值`w*,b*`，得出分离超平面和分类决策函数。

#### 2. 线性支持向量机

* 训练数据近似线性可分，使用线性支持向量机，或软间隔支持向量机。

  * 引入松弛变量ξi，使其‘’可分‘’，最优化原始问题

    ![](D:\下载\CodeCogsEqn (7).gif)

    ![](D:\下载\CodeCogsEqn (8).gif)

    ![](D:\下载\CodeCogsEqn (9).gif)

    * 求解原始最优化问题的解`w*,b*`，得到线性支持向量机，分离超平面为

    ![](D:\下载\CodeCogsEqn (5).gif)

    * 分类决策函数为

    ![](D:\下载\CodeCogsEqn (6).gif)

    线性支持向量机的解`w`唯一但`b*`不一定唯一。

  * 对偶问题为

    ![](D:\下载\CodeCogsEqn (10).gif)

    ![](D:\下载\CodeCogsEqn (11).gif)

    ![](D:\下载\CodeCogsEqn (12).gif)

    * 通过求解对偶问题学习线性可分支持向量机，首先求得最优值`a*`,然后求最优值`w*,b*`，得出分离超平面和分类决策函数。
    * 对偶问题的解a*中满足a*i>0的实例点xi称为支持向量。支持向可在间隔边界上，也可在间隔边界与分离超平面之间，或者在分离超平面误分的一侧。最优分离超平面由支持向量完全决定。
    * 线性支持向量机学习等价于最小化二阶范数正则化的合页函数

    ![](D:\下载\CodeCogsEqn (13).gif)

    #### 3. 非线性支持向量机

* 对于输入空间中的非线性分类问题，可以通过非线性变换将它转化为某个高维特征空间中的线性分类问题。用核函数替代内积。核函数表示通过一个非线性变换后的两个实例间的内积。

  * 核函数

    * K(x,z)是一个核函数，或正定核，存在一个从输入空间X到特征空间H的映射 φ(x)，对任意x,z有

      K(x,z) = φ(x)*φ(z)

      对称函数K(x,z)为正定核的充要条件为：对任意x，对称函数K(x,z)对应的Gram矩阵是半正定的。

    * 所以用核函数表示内积，求得的非线性支持向量机

      ![](D:\下载\CodeCogsEqn (14).gif)

#### 4. SMO算法

* SMO算法特点是不断将原二次规划问题分解为只有两个变量的二次规划子问题，并对子问题进行解析求解，直到所有变量满足KKT条件为止。

* 仿射函数

  * 若`f(x)`满足`f(x)=ax+b`，则称`f(x)`为放射函数。

* 凸二次规划问题

  * 凸函数
    * 函数任意两点连线处的值大于对应自变量处的函数值。

  * 凸优化

    * 要求目标函数是凸函数，变量所属集合是凸集合优化问题 

  * 函数表示
    $$
    \min_{x}q(x)=\frac{1}{2}x^TGx+x^Tc
    $$

    $$
    s.t.a_i^Tx\geq b_i,i\euro \tau
    $$

    * G是Hessian矩阵，T是有限指标集。如果Hessian矩阵是半正定矩阵，则我们说该式是一个凸二次规划。常用拉格朗日求解凸二次规划问题。

* 拉格朗日函数
  $$
  minf(x)
  $$

  $$
  s.t.g_I(x)\leq 0
  $$

  $$
  h_i(x)\leq 0
  $$

  $$
  L(x,\alpha ,\beta )=f(x)+\sum_{i=1}^{n}\alpha _ig(x)+\sum_{i=1}^{n}\beta _ih(x)
  $$

  

- KKT条件：

  - 主问题可行
    $$
    g(x)≤ 0
    $$

  - 对偶问题可行
    $$
    aα_i≥0
    $$

  - 互补松弛
    $$
    α_ig(x)=0
    $$
