---
date: 2024-11-04
tags:
  - 机器学习
  - 聚类
  - K-Means
---
# K-Means++
## 什么是k-means++
**K-means++** 是一种改进的质心初始化方法，用来解决 K-means 聚类算法对初始质心敏感的问题。通过 K-means++ 的初始化方式，可以使 K-means 更加稳定、快速地收敛，同时提高找到全局最优解的可能性。
## k-means++的主要思想
在选择灭一个新的初始质心时，<mark>优先选择离已有质心较远的点</mark>，这样可以确保初始质心尽量分散，覆盖数据的主要区域，从而减少迭代次数，降低陷入局部最优解的可能性。
## 为什么k-means++有效
首先可以看一组对比图：
![[output.png]]
1. 减少了局部最优的风险：K-means 的随机初始化容易导致质心集中在数据的某个局部区域，导致算法陷入局部最优。K-means++ 通过让质心分散，从而增加找到全局最优解的可能性。
2. 加速收敛：初始质心更合理时，数据点会更接近其正确的簇，减少了算法调整质心位置的工作量，从而加快收敛。
3. 平衡簇的大小：通过选择离现有质心较远的数据点作为新的质心，K-means++ 在初始化时就确保簇分布较均匀，避免出现某些簇过大或过小的情况。
## k-means++的步骤
1. 随机选择第一个质心：从数据集中选择一个数据点作为第一个质心。
2. 计算每个数据点到最近质心的距离记为D(x)。同k-means，这篇文章当中有讲到这一点[[机器学习之聚类算法]]
3. 概率选择下一个质心
	1. 选择下一个质心时，不是完全随机选择，而是根据距离的平方来确定选择的概率。
	2. 将每个数据点x以D(x)的平方作为概率选择为下一个质心，具体来说，距离越远的点有更高的概率被选为新的质心。
4. 重复2和3，直到选择了K个质心。
5. 开始标准的K-means迭代：使用初始化得到的K个质心，按照标准的K-means算法进行迭代，直到算法收敛。
## 代码实现
这里实现最关键的<mark>确定质心</mark>
```python
import numpy as np

def initialize_centroids_kmeans_pp(X, K):
    """
    使用 K-means++ 方法初始化质心.
    
    参数:
    - X: 数据集 (numpy array)，形状为 (n_samples, n_features)
    - K: 需要生成的簇数
    
    返回值:
    - centroids: 初始化的 K 个质心，形状为 (K, n_features)
    """
    # 获取样本数和特征数
    n_samples, n_features = X.shape
    
    # 初始化一个空的质心数组
    centroids = np.zeros((K, n_features))
    
    # 随机选择第一个质心
    centroids[0] = X[np.random.randint(0, n_samples)]
    
    # 选择接下来的质心
    for i in range(1, K):
        # 计算每个数据点到最近已选质心的距离平方
        distances = np.min([np.linalg.norm(X - centroid, axis=1)**2 for centroid in centroids[:i]], axis=0)
        
        # 依据距离平方，按比例选择下一个质心
        probabilities = distances / distances.sum()
        cumulative_probabilities = np.cumsum(probabilities)
        r = np.random.rand()
        next_centroid_idx = np.where(cumulative_probabilities >= r)[0][0]
        
        # 将选中的数据点作为下一个质心
        centroids[i] = X[next_centroid_idx]
    
    return centroids
```