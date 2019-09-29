## N-th Tribonacci Numbert

题目描述：

The Tribonacci sequence Tn is defined as follows: 

T0 = 0, T1 = 1, T2 = 1, and Tn+3 = Tn + Tn+1 + Tn+2 for n >= 0.

Given `n`, return the value of Tn.

**Constraints:**

- `0 <= n <= 37`
- The answer is guaranteed to fit within a 32-bit integer, ie. `answer <= 2^31 - 1`.

分析：

1. 递归类问题，由题目可得递归式：
   $$
   T(n) = T(n - 3) + T(n - 2) + T(n - 1)
   $$

   $$
   T0 = 0;
   T1 = 1;
   T2 = 1;
   $$

    由递归式转函数，可以第二行作为首先判断的递归出口，递归式右侧内容直接作为其他情况的return内容。

2. 代码书写：

   1> 首先想到递归，但有重复计算速度太慢，没有通过。

```c
int tribonacci(int n){
    if (n < 2) return n;
    if (n == 2) return 1;
    
    return tribonacci(n - 3) + tribonacci(n - 2) + tribonacci(n - 1); 
}
```

​	2> 优化递归性能，可以用动态规划，记录中间结果：

```c
int tribonacci(int n){
    int T[37 + 1] = {0};
    int m;
    if (n < 2) return n;
    if (n == 2) return 1;
    
    T[0] = 0;
    T[1] = 1;
    T[2] = 1;
    
    for (m = 3; m <= n; m++) {
        T[m] = T[m - 3] + T[m - 2] + T[m - 1];
    }
    return T[n];
    
}
```

​	3>  减少局部变量的空间使用，由评论区得另外一种解法：

```c
int tribonacci(int n){
    if (n < 2) return n;
    if (n == 2) return 1;
    int x = 0;
    int y = 1;
    int z = 1;
    int a = x + y + z;
    
    while (--n > 2) {
        x = y;
        y = z;
        z = a;
        a = x + y + z;
    }
    return a;
    
}
```

