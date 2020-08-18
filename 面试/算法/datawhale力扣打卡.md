## Task01：分治（2天）

#### [50. Pow(x, n)](https://leetcode-cn.com/problems/powx-n/)

根据递归计算的结果，如果 nn 为偶数，那么 x^n = y^2;
如果 nn 为奇数，那么 x^n = y^2 * x;

```python
class Solution:
    def myPow(self, x: float, n: int) -> float:      
        judge = True
        if n < 0:
            n = -n
            judge = False      
        final = 1
        while n>0:
            if n & 1:   #代表是奇数
                final *= x
            x *= x
            n >>= 1     # 右移一位
        return final if judge else 1/final
```



####  [53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

1. 暴力法: 当前面序列sum>0时 继续加num

```python
class Solution:
    def maxSubArray(self, nums: List[int]) -> int:
        sum_,ans = 0,nums[0]
        for num in nums:
            if sum_ >= 0:
                sum_ += num
            else:
                sum_ = num
            ans = max(sum_,ans)
        return ans
```

2. 分治法

#### [169. 多数元素](https://leetcode-cn.com/problems/majority-element/)

```python
class Solution:
    def majorityElement(self, nums: List[int]) -> int:
        d = {}
        for num in nums:
            d[num] = d.get(num,0) + 1
        return max(d.items(),key = lambda item:item[1])[0]
```



