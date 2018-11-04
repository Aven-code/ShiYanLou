# 最短路径问题 shortest path problem

## 问题解释： 

从图中的某个顶点出发到达另外一个顶点的所经过的边的权重和最小的一条路径，称为最短路径

## 解决问题的算法：

1. 迪杰斯特拉算法（Dijkstra算法）

2. 弗洛伊德算法（Floyd算法）

3. SPFA算法

## 1. Dijkstra算法介绍
[参考](https://blog.csdn.net/qq_35644234/article/details/60870719)

### 算法特点：
      迪科斯彻算法使用了广度优先搜索解决赋权有向图或者无向图的单源最短路径问题，
      算法最终得到一个最短路径树。
      该算法常用于路由算法或者作为其他图算法的一个子模块。

### 算法的思路

      Dijkstra算法采用的是一种贪心的策略，声明一个数组dis来保存源点到各个顶点的最短距离和
      一个保存已经找到了最短路径的顶点的集合：T，初始时，原点 s 的路径权重被赋为 0 （dis[s] = 0）。
      若对于顶点 s 存在能直接到达的边（s,m），则把dis[m]设为w（s, m）,同时把所有其他（s不能直接到达的）
      顶点的路径长度设为无穷大。初始时，集合T只有顶点s。 
      然后，从dis数组选择最小值，则该值就是源点s到该值对应的顶点的最短路径，
      并且把该点加入到T中，OK，此时完成一个顶点， 
      然后，我们需要看看新加入的顶点是否可以到达其他顶点并且看看通过该顶点到达其他点的路径长度是否比源点直接到达短，
      如果是，那么就替换这些顶点在dis中的值。 
      然后，又从dis中找出最小值，重复上述动作，直到T中包含了图的所有顶点。

## 2. Floyd算法的介绍
[参考](https://blog.csdn.net/qq_35644234/article/details/60875818)

### 算法的特点： 
      弗洛伊德算法是解决任意两点间的最短路径的一种算法，
      可以正确处理有向图或有向图或负权（但不可存在负权回路)的最短路径问题，
      同时也被用于计算有向图的传递闭包。

## 算法的思路

      通过Floyd计算图G=(V,E)中各个顶点的最短路径时，需要引入两个矩阵，
      矩阵S中的元素a[i][j]表示顶点i(第i个顶点)到顶点j(第j个顶点)的距离。
      矩阵P中的元素b[i][j]，表示顶点i到顶点j经过了b[i][j]记录的值所表示的顶点。

      假设图G中顶点个数为N，则需要对矩阵D和矩阵P进行N次更新。
      初始时，矩阵D中顶点a[i][j]的距离为顶点i到顶点j的权值；
      如果i和j不相邻，则a[i][j]=∞，矩阵P的值为顶点b[i][j]的j的值。 
      接下来开始，对矩阵D进行N次更新。
      第1次更新时，如果”a[i][j]的距离” > “a[i][0]+a[0][j]”(a[i][0]+a[0][j]表示”i与j之间经过第1个顶点的距离”)，
      则更新a[i][j]为”a[i][0]+a[0][j]”,更新b[i][j]=b[i][0]。 
      同理，第k次更新时，如果”a[i][j]的距离” > “a[i][k-1]+a[k-1][j]”，
      则更新a[i][j]为”a[i][k-1]+a[k-1][j]”,b[i][j]=b[i][k-1]。
      更新N次之后，操作完成！



## 3. SPFA算法介绍
[最短路径问题---SPFA算法详解](https://blog.csdn.net/qq_35644234/article/details/61614581)

      SPFA算法是求解单源最短路径问题的一种算法，由理查德·贝尔曼（Richard Bellman） 和 莱斯特·福特 创立的。
      有时候这种算法也被称为 Moore-Bellman-Ford 算法，因为 Edward F. Moore 也为这个算法的发展做出了贡献。
      它的原理是对图进行V-1次松弛操作，得到所有可能的最短路径。
      其优于迪科斯彻算法的方面是边的权值可以为负数、实现简单，
      缺点是时间复杂度过高，高达 O(VE)。但算法可以进行若干种优化，提高了效率。

      算法的思路： 
      我们用数组dis记录每个结点的最短路径估计值，用邻接表或邻接矩阵来存储图G。
      我们采取的方法是动态逼近法：设立一个先进先出的队列用来保存待优化的结点，
      优化时每次取出队首结点u，并且用u点当前的最短路径估计值对离开u点所指向的结点v进行松弛操作，
      如果v点的最短路径估计值有所调整，且v点不在当前的队列中，就将v点放入队尾。
      这样不断从队列中取出结点来进行松弛操作，直至队列空为止

      我们要知道带有负环的图是没有最短路径的，所以我们在执行算法的时候，要判断图是否带有负环，方法有两种：

      开始算法前，调用拓扑排序进行判断（一般不采用，浪费时间）
      如果某个点进入队列的次数超过N次则存在负环（N为图的顶点数）