---
layout: post
title:  Leetcode算法题 接雨水 解法总结
---
## 给定 n 个非负整数表示每个宽度为 1 的柱子的高度图，计算按此排列的柱子，下雨之后能接多少雨水。
![piture](/images/rainwatertrap.png)
### 解法一:韦恩图
 '''
 class Solution(object):
    def trap(self, height):
        sum_of_left, sum_of_right = 0, 0
        max_left, max_right = 0, 0
        n=len(height)
        for i in range(n):
            if height[i] > max_left:
                max_left = height[i]
            if height[n- i -1] > max_right:
                max_right = height[n - i - 1]
            sum_of_left += max_left
            sum_of_right += max_right
        volume = sum_of_left + sum_of_right - max_left * len(height) - sum(height)
        return volume
'''
## 解法二:单指针 暴力超时解
'''
class Solution:
    def trap(self, height):
        ans = 0
        for i in range(len(height)):
            max_left, max_right = 0,0
            # 遍历位置i左边的柱子寻找 max_left
            for j in range(0,i):
                max_left = max(max_left,height[j])
            # 遍历位置i右边的柱子寻找 max_right
            for j in range(i,len(height)):
                max_right = max(max_right,height[j])
            #print('max_right='+str(max_right),'max_left='+str(max_left),'height_i='+str(height[i]))

            if min(max_left,max_right) > height[i]:
                ans += min(max_left,max_right) - height[i]  
        return ans
'''
## 解法三：双指针
'''
class Solution:
    def trap(self, height):
        ans = 0
        left, right = 0, len(height) - 1
        leftMax = rightMax = 0
        while left < right:
            leftMax = max(leftMax, height[left])
            rightMax = max(rightMax, height[right])

            if height[left] < height[right]:
                ans += leftMax - height[left]
                left += 1  
            else:
                ans += rightMax - height[right]
                right -= 1      
        return ans
'''
 **难点： 每一个位置可以积累的水量由什么确定？**
 **由 左右两边柱子的最低点与当前柱子的高度差决定**










<!-- 

Next you can update your site name, avatar and other options using the _config.yml file in the root of your repository (shown below).

![_config.yml]({{ site.baseurl }}/images/config.png)

The easiest way to make your first post is to edit this one. Go into /_posts/ and update the Hello World markdown file. For more instructions head over to the [Jekyll Now repository](https://github.com/barryclark/jekyll-now) on GitHub.  -->