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



## 动态规划

#### [Leetcode 674.最长连续递增序列](https://leetcode-cn.com/problems/longest-continuous-increasing-subsequence/)

```python
def findLengthOfLCIS(self, nums: List[int]) -> int:
        if not nums:return 0 
        dp=[1]*len(nums)     
        for i in range(1,len(nums)): 
        	if nums[i]>nums[i-1]:
                    dp[i]=dp[i-1]+1
                else:
                    dp[i]=1
        return max(dp)
```

#### [Leetcode5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

```java
class Solution {
    public String longestPalindrome(String s) {
        if (s == null || s.length() == 0) return "";
        int L = 0, R = 0;
        for (int i = 0; i < s.length(); i++){
            int len1 = getPalindromeLen(s, i, i);
            int len2 = getPalindromeLen(s, i, i + 1);
            int len = Math.max(len1, len2);
            if (len > R - L){
                L = i - (len - 1) / 2;
                R = i + len / 2;
            }
        }
        return s.substring(L, R+1);
    }
    private int getPalindromeLen(String s, int l, int r) {
            while (l >= 0 && r <s.length() && s.charAt(l) == s.charAt(r)){
                l--;
                r++;
            }
            return r - l -1;
        }
}
```

#### [Leetcode72. 编辑距离](https://leetcode-cn.com/problems/edit-distance/)

```python
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        len1, len2 = len(word1),len(word2)
        if len1*len2 == 0: return len1+len2
        dp = [[0]*(len2+1) for _ in range(len1+1)]
        for i in range(len1+1):
            dp[i][0] = i
        for j in range(len2+1):
            dp[0][j] = j
        
        for i in range(1,len1+1):
            for j in range(1,len2+1):
                lastlast = 1 if word1[i-1] != word2[j-1] else 0
                dp[i][j] = min(dp[i-1][j]+1,dp[i][j-1]+1, dp[i-1][j-1]+lastlast)
        # print(dp)
        return dp[-1][-1]
```

