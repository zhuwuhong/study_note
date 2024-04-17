# 刷题笔记

#### 二分法

```python
'''
在未知多个版本中找出第一个错误版本
例如 1 2 3个版本中2和3是错误版本，那么要找出的应该是2这个错误版本
'''
class Solution(object):
    def firstBadVersion(self, n):
        """
        :type n: int
        :rtype: int
        """
        left, right = 1,n
        while left <=right:
            mid = (left+right)//2 # 取中间值
            if isBadVersion(mid) == True: #如果中间是的话则去看中间值的上一位是否是错误版本
                if isBadVersion(mid-1) == False: #如果中间值得上一位不是那么就直接抛出中间值
                    return mid
                else: #如果中间值得上一位是错误版本的话
                    right = mid #收束右边界
            elif isBadVersion(mid) == False: #如中间值不是错误版本则收束左边界
                left = mid +1 
        return mid
```

```python
'''
给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。
请必须使用时间复杂度为 O(log n) 的算法。
'''
二分法解法：
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        left,right = 1,len(nums)-1 #初始化左右边界
        while left <= right:
                mid = (left+right)//2 # 找出中间值
                if nums[mid] < target: # 如果列表中的中间值小于插值那么就收束左值
                    left = mid+1 # 防止中间值出现同一值
                elif nums[mid] > target: # 如果列表中的中间值大于插值那么就收束左值
                    right = mid-1 # 防止中间值出现同一值
                else: # 如果列表中的中间值等于插值那么直接抛出中间值的下标
                    return mid 
        return right + 1 # 当left大于right时就代表这个值不存在因此再右边界外添加这个值
暴力解法：
class Solution(object):
    def searchInsert(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: int
        """
        # 如果遍历了一遍所有值他都没有出现nums[i]>=target这个情况则代表target比nums里所有的值都大，因此输出len(nums)
        for i in range(0,len(nums)-1):
            if (nums[i] >= target):
                return i
        if len(nums) != 1 or nums[0] < target:
            return len(nums)
        else:
            return 0
```

#### 计算题

```py	
"""
公鸡5块钱一只
母鸡3块钱一直
消极3只一块钱
现在用100块钱买了100只鸡有那些买法
"""
re = [('公鸡:',cock,'母鸡:',hen,'小鸡:',chick)
      # 枚举100块钱可以买的公鸡数
      for cock in range(20+1)
      # 枚举100块钱可以买的母鸡数
      for hen in range(33+1)
      # 枚举100块钱可以买的小鸡数
      for chick in range(300+1)
      # 满足100元买100只鸡的可能且小鸡一定要被3整除才能添加到列表中
      if (cock + hen + chick == 100 and 5 * cock + 3 * hen + chick // 3 == 100) and chick % 3 ==0]
print(re)
```

