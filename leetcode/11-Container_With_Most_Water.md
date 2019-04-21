## 11. Container With Most Water

### 1.  题目信息：

题目地址：**https://leetcode.com/problems/container-with-most-water/

**题目描述：**

Given *n* non-negative integers *a1*, *a2*, ..., *an* , where each represents a point at coordinate (*i*, *ai*). *n* vertical lines are drawn such that the two endpoints of line *i* is at (*i*, *ai*) and (*i*, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and *n* is at least 2.

![img](https://s3-lc-upload.s3.amazonaws.com/uploads/2018/07/17/question_11.jpg)

The above vertical lines are represented by array [1,8,6,2,5,4,8,3,7]. In this case, the max area of water (blue section) the container can contain is 49.

大意为给出一个有n个元素的数组，数组其中每个元素代表着高度(y)，各个元素的间距为1。求其中任意两个元素可在坐标轴中可围成的最大面积。需要注意的是，在取高度时，只能取两个元素中的最小值。

### 2.  解题代码：

欻欻解法：

最容易想到的是两次遍历，先以其中一边为基准，遍历另一个边，复杂度为O(n^2):

```c
int maxArea(int* height, int heightSize) {
    
    int l, h;
    int area=0;
    int *tail = height + heightSize;
    
    for (int *start = height; start < tail; start++)
    {
        for (int *end = start + 1, l = 1; end < tail; end++, l++)
        {
            h = *end < *start ? *end : *start;
            area = (h * l) > area ? (h * l) : area;
        }
    }
    
    return area;
}
```

跑出来的时间和占用空间为：368ms 7.7mb

正确解法：

复杂度O(n)：

```c
int maxArea(int* height, int heightSize) {
    
    int left = 0;
    int right = heightSize - 1;
    int area = 0;
    int s = 0;

    while(left < right)
    {   
        s = ((*(height + left) > *(height + right)) ? height[right--] : height[left++]) * (right - left + 1);
        area = s > area ? s : area;        
    }
    
    return area;
}
```

运行时间：8ms 占用空间：7.8mb