# 刷题日志



### String 


---

### Binary Search


---


### Binary Tree












---
### DP 
Advantage:
1. 不重复计算
2. 按顺序算

Usage:
1. 找最大最小值
2. **判断是否可行**
3. **统计方案个数**

什么情况下不能用DP?
* 上下左右四个方向都可以走的，一般就不是动态规划了（**状态之间不会存在循环引用**）
* DP的输入数据不是集合，必须是序列，其实本质说的是，必须是按照一个方向一个顺序从左到右或者从上到下的。所以在矩阵上，如果是四个方向都可以走，就会形成环状依赖关系的，那么就一定不是动态规划了。
* 求具体方案


DP分类
* **单序列**：一般是 前 i个。也就是说，是一个前缀，包含i-1,i-2,i-3 .. 是一大坨东西。

  单序列的话。就考虑这个前缀所包含的子前缀。
* **坐标**： 一般是我跳到了第i个位置，不包含i-1,i-2,i-3 ...是单个的东西。（想象一个小人在跳来跳去）
  
  坐标的话的，就思考上一步在哪儿

---

### LinkedList




---


### Arrays & Numbers
**二维数组转一维**
* 都与列的个数有关
* ```/ ```用来纵向移动，```%```用来横向移动
* 一个m*n的2d matrix, 每个点的坐标为```(x,y)```, 
* **id = x*n + y**
* 1d=>2d: **x = id / n**， **y = id % n**





 
 




---


### Data Structure



---

### Graph & Search



---

## **Two Pointer**









































































