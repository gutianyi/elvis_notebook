# Code Algorithm
[TOC]
---
### key points
* 右移一位相当于除2，右移n位相当于除以2的n次方。这里是取商哈，余数就不要了。(java 里面用>>表示 eg: `intNum >> 1` )

  
### search(查找)
#### 二分查找

```python
def lower_bound(array, first, last, value): # 返回[first, last)内第一个不小于value的值的位置
  while first < last: # 搜索区间[first, last)不为空
    mid = first + (last - first) // 2 # 防溢出
    if array[mid] < value: first = mid + 1
      else: last = mid
  return first # last也行，因为[first, last)为空的时候它们重合
```

```python
# 针对左闭右开
def findValue(array, first, last, value): #给定一个有序的数组，查找value是否在数组中，不存在返回-1。
  while (first < right){
    mid = first + (last - first) // 2 # 防溢出
    if array[mid] < value :
    	first = mid + 1
    elif array[mid] > value:
    	last = mid
    else:
    	return mid
  }
	return -1
```



