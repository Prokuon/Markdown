# 力扣题解

## 位运算

### [2044](https://leetcode-cn.com/problems/count-number-of-maximum-bitwise-or-subsets/) 统计按位或能得到最大值的子集数目

```c++
class Solution 
{
public:
    int countMaxOrSubsets(vector<int>& nums)
    {
        int n = nums.size(), maxValue = 0, cnt = 0, stateNumber = 1 << n;
        for (int i = 0; i < stateNumber; i++)
        {
            int cur = 0;
            for (int j = 0; j < n; j++)
            {
                if (((i >> j) & 1) == 1) // 二进制枚举？
                {
                    cur |= nums[j];
                }
            }
            if (cur == maxValue)
            {
                cnt++;
            } 
            
            else if (cur > maxValue)
            {
                maxValue = cur;
                cnt = 1;
            }
        }
        return cnt;
    }
};
```

上述代码循环与判断部分似乎是用于进行C排列？

二进制枚举法：

> 记 n 是数组 nums 的长度，数组中的每个元素都可以选取或者不选取，因此数组的非空子集数目一共有 $(2^n - 1)$个。可以用一个长度为 n 比特的整数来表示不同的子集，在整数的二进制表示中，n 个比特的值代表了对数组不同元素的取舍。第 i 位值为 1 则表示该子集选取对应元素，第 i 位值为 0 则表示该子集不选取对应元素。求出每个子集的按位或的值，并计算取到最大值时的子集个数。

### [693](https://leetcode-cn.com/problems/binary-number-with-alternating-bits/) 交替位二进制数

```c++
class Solution 
{
public:
    bool hasAlternatingBits(int n) 
    {
        long a = n ^ (n >> 1);
        return (a & (a + 1)) == 0;
    }
};
```

## 前缀和

### [528](https://leetcode-cn.com/problems/random-pick-with-weight/) 按权重随机选择

```c++
class Solution 
{
private:
    mt19937 gen;
    uniform_int_distribution<int> dis;
    vector<int> pre;

public:
    Solution(vector<int>& w): gen(random_device{}()), dis(1, accumulate(w.begin(), w.end(), 0)) 
    {
        partial_sum(w.begin(), w.end(), back_inserter(pre));
    }
    
    int pickIndex() 
    {
        int x = dis(gen);
        return lower_bound(pre.begin(), pre.end(), x) - pre.begin();
    }
};
```

STL说明：

> 1. mt19937 头文件是 <random> 是伪随机数产生器，用于产生高性能的随机数
> 2. uniform_int_distribution 头文件在 <random> 中，是一个随机数分布类，参数为生成随机数的类型，构造函数接受两个值表示区间段
> 3. accumulate 头文件在 <numeric> 中，求特定范围内所有元素的和。
> 4. spartial_sum 函数的头文件在 <numeric>，对 (first, last) 内的元素逐个求累计和，放在 result 容器内
> 5. back_inserter 函数头文件 <iterator>，用于在末尾插入元素。
> 6. lower_bound 头文件在 <algorithm>，用于找出范围内不小于 num 的第一个元素

### [1109](https://leetcode-cn.com/problems/corporate-flight-bookings/) 航班预订统计

```c++
class Solution 
{
public:
    vector<int> corpFlightBookings(vector<vector<int>>& bookings, int n) 
    {
        vector<int> nums(n);
        for (auto booking : bookings)
        {
            nums[booking[0] - 1] += booking[2];
            if (booking[1] < n)
            {
                nums[booking[1]] -= booking[2];
            }
        }
        for (int i = 1; i < n; i++)
        {
            nums[i] += nums[i - 1];
    
        }
        return nums;
    }
};
```

差分数组：

> 差分数组对应的概念是前缀和数组，对于数组 \[1,2,2,4]，其差分数组为 \[1,1,0,2]，差分数组的第$i$个数即为原数组的第$i-1$个元素和第$i$个元素的差值，也就是说我们对差分数组求前缀和即可得到原数组。
>
> 差分数组的性质是，当我们希望对原数组的某一个区间 \[l,r] 施加一个增量$inc$时，差分数组$d$对应的改变是：$d[l]$增加$inc$，$d[r+1] $减少$inc$。这样对于区间的修改就变为了对于两个位置的修改。并且这种修改是可以叠加的，即当我们多次对原数组的不同区间施加不同的增量，我们只要按规则修改差分数组即可。

## 递归

### [剑指 Offer 64](https://leetcode-cn.com/problems/qiu-12n-lcof/) 求 1+2+…+n

```c++
class Solution {
public:
    int sumNums(int n) {
        n && (n += sumNums(n-1));
        return n;
    }
};
```

> 利用逻辑运算符的短路性质

### [1823](https://leetcode-cn.com/problems/find-the-winner-of-the-circular-game/) 找出游戏的获胜者

```c++
class Solution 
{
public:
    int findTheWinner(int n, int k) 
    {
        if(n == 1) 
            return 1;
        int ans = findTheWinner(n - 1, k) + k;
        return ans % n == 0 ? n : (ans % n);
    }
};
```

思路详解

> 定义：从 1 到 N 编号每 k 个淘汰一个，游戏结束时的幸存者编号为 f (N, k)。
>
> 在 N 个人中首先淘汰的必然是第 k 号，其最终幸存者，就是剩余 N-1 个人继续游戏的最终幸存者
> 而剩余 N-1 个人将以第 (k+1) 号作为游戏的起点（这是一句废话！）
> 若以第 (k+1) 号作为第 1 号，剩余 N-1 个人在新的编号规则下的幸存者就是 f (N-1, k)（递归函数定义）
>
> 现已知，剩余 N-1 个人在新的编号规则下的幸存者编号是 f (N-1, k)，
> 这个编号就是已知的，因为这是递归！是递归！递归！怎么算的交给 f (N-1, k) 的内部递归过程，此处就是任性直接用！
>
> 接下来就是怎么把新的编号规则下的确定编号 f (N-1, k)，转换为原来 1~N 编号规则下的编号
> 新编号规则下的 1 号是原来的 k+1 号，新编号规则的 2 号是原来的 k+2 号，...，新编号规则下的 N-k 号是原来的 N 号，新编号规则下的 N-k+1 号是原来的 1 号，... ...
> 因此，新编号规则下的编号加上 k 即为原来的编号，若加上 k 之后超过了 N 说明超过了原始编号规则中的最后一个 (又从 1 开始了)，直接减去 N 即可，即 f (n, k) = f (n-1, k) + k（若其超过 N 则需减去 N）。
>
> 另外，此处的 k 是有可能超过 n 的很多倍的，因此 f (n-1, k) 加上 k 后应该去掉 N 的整数倍后取剩余部分
> 此处不能直接取余，因为 N 的倍数时在本题的含义应该是第 N 号 (取余之后会变成 0 号)，完整的逻辑表述如下：
> f (n, k) 的值 ans 应为 f (n-1, k) + k，若 ans 不超过 N 则直接为 N，超过 N 之后继续从 1 编号，最终得到的小于等于 N 的即为答案；
> 也即 ans 对 N 取余，不能整除直接就是答案，能整除就是 N。

### [面试题 08.06](https://leetcode-cn.com/problems/hanota-lcci/) 汉诺塔问题

```c++
class Solution 
{
public:
    void move(vector<int>& a, vector<int>& b, vector<int>& c, int n) 
    {
        if (n == 1)
        {
            c.push_back(a.back());
            a.pop_back();
            return;
        }
        move(a, c, b, n - 1);
        move(a, b, c, 1);
        move(b, a, c, n - 1);
    }

    void hanota(vector<int>& a, vector<int>& b, vector<int>& c) 
    {
        move(a, b, c, a.size());
    }
};
```

## 二叉树

### [101](https://leetcode-cn.com/problems/symmetric-tree/) 对称二叉树

```c++
class Solution 
{
public:
    bool check(TreeNode* rf, TreeNode* rr)
    {
        if (!rf && !rr)
            return true;
        if (!rf || !rr)
            return false;
        return rf->val == rr->val && check(rf->right, rr->left) && check(rf->left, rr->right);
    }

    bool isSymmetric(TreeNode* root) 
    {
        return check(root, root);
    }
};
```

### [236](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)  二叉树的最近公共祖先

```c++
class Solution
{
private:
    TreeNode* ans;
    bool dfs(TreeNode* root, TreeNode* p, TreeNode* q)
    {
        if (!root)
            return false;
        bool lft = dfs(root->left, p, q);
        bool rgt = dfs(root->right, p, q);
        if ((lft && rgt) || ((root->val == p->val || root->val == q->val) && (lft || rgt)))
            ans = root;
        return (lft || rgt || root->val == p->val || root->val == q->val);
    }
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) 
    {
        dfs(root, p, q);
        return ans;
    }
};
```

> 思路和算法
>
> 我们递归遍历整棵二叉树，定义 $f_x$ 表示 x 节点的子树中是否包含 p 节点或 q 节点，如果包含为` true`，否则为` false`。那么符合条件的最近公共祖先 x 一定满足如下条件：
> $$
> (f_{\text{lson}}\ \&\&\ f_{\text{rson}})\ ||\ ((x\ =\ p\ ||\ x\ =\ q)\ \&\&\ (f_{\text{lson}}\ ||\ f_{\text{rson}}))
> $$
> 其中 $\text{lson}$ 和 $\text{rson}$ 分别代表 x 节点的左孩子和右孩子。初看可能会感觉条件判断有点复杂，我们来一条条看， $f_{\text{lson}}\ \&\&\ f_{\text{rson}}$ 说明左子树和右子树均包含 p 节点或 q 节点，如果左子树包含的是 p 节点，那么右子树只能包含 q 节点，反之亦然，因为 p 节点和 q 节点都是不同且唯一的节点，因此如果满足这个判断条件即可说明 x 就是我们要找的最近公共祖先。再来看第二条判断条件，这个判断条件即是考虑了 x 恰好是 p 节点或 q 节点且它的左子树或右子树有一个包含了另一个节点的情况，因此如果满足这个判断条件亦可说明 x 就是我们要找的最近公共祖先。

## 随机数

### [398](https://leetcode-cn.com/problems/random-pick-index/) 随机数索引

## 背包问题

### 01背包问题

```c++
/*
result = max{f[n][0-v]}
f{[i][j]}:
1. 不选第i个物体：f[i][j] = f[i - 1][j]
2. 选第i个物体：f[i][j] = f[i - 1] - v[i]
f[i][j] = max{1, 2}
f[0][0] = 0
*/

```



### 完全背包问题

### 多重背包问题

### 混合背包问题

### 二维费用的背包问题

### 分组背包问题

### 背包问题求方案数

### 求背包问题的方案

### 有依赖的背包问题





