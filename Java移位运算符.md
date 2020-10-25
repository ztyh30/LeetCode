# Java移位运算符

## 191.位1的个数

![191.位1的个数（1）](D:\TyporaNote\力扣\191.位1的个数（1）.png)

![191.位1的个数（2）](D:\TyporaNote\力扣\191.位1的个数（2）.png)

首先，先说一下java的三种移位运算符：

* `<<`：左移运算符（高位舍去，低位补零）
* `>>`：右移运算符（高位补符号位，低位舍去）
* `>>>`：无符号右移运算符，忽略符号位，空位补0

解法：把n向右移位32次，每次与1做与运算

```java
public int hammingWeight(int n) {
    int count = 0;
    for (int i = 0; i < 32; i++) {
        if (((n >>> i) & 1) == 1) {
            count++;
        }
    }
    return count;
}
```

优化：

```java
public int hammingWeight(int n) {
    int count = 0;
    while (n != 0) {
        count += n & 1;
        n = n >>> 1;
    }
    return count;
}
```

**每次消去最右边的1，知道消完所有1**

比如有一个数的二进制为`n = xxx10000`，那么`n - 1`就等于`xxx01111`（二进制减法）

这样`n`与`n-1`进行与运算（&），得`n & n-1 = xxx00000`，相当于把一开始最右边的1给消掉了，循环这个操作，直到`n`等于0，循环了几次，就代表有多少个`n`有几个1

代码：

```java
 public int hammingWeight(int n) {
        int count = 0;
        while(n != 0) {
            n &= n - 1;
            count++;
        }
        return count;
    }
```

