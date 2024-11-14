---
title: 有限自动机总结速递.md
date: 2024-11-14 15:25:51
tags:
  - Computer science
categories:
  - Compression algorithms
  - Final review
  - Discipline Summary
---

# 第三章 有限状态自动机
接收右线性文法（也叫正则文法，三型文法），特点是左比右少，左只有一个非终结符，右如果有非终结符的话只在最右边出现。
## DFA确定有限状态自动机

### 绘制流程
**例3.0**构造DFA，接收{0，1}上的语言L={x000y|x，y∈{0，1}}。
#### 确定基本结构
基本结构（接收基本句子000）的状态转移函数为
$δ(qo, 0) =q1, δ(q1, 0)=q2, δ(q2,0)=q3$
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111546474.png)

#### 补全所有分支
4个状态，DFA要求每个状态对每个可能的串都要有且仅有一种转移，也就是4\*2=8个转移线，基本结构中只有3条，故补全5条，每个状态都要有2条以自己为起点的转移。
	这里的2指的是字母表里只有2个字母，因此下一个字符只有2种可能
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111547090.png)

##### 双圈与陷阱状态qt的理解
	输入串扫描结束时，DFA将自动停机。这是DFA停机的唯一情况。注意
	（1）DFA将输入串扫描结束停机时，若处于某一个接收状态，则表示接收整个输入串；DFA将输入串扫描结束停机时，若未处于任何接收状态，则表示不接收整个输入串。
	（2）DFA的某个状态q，若不能接收字母表上的字母x，则需要定义一个特殊的状态：陷阱状态q1，q1不能转变为其他状态
	（3）当允许空串时，q0画上双圈。幂的位置是*是含空串，是+则不含。
### 例题
**例3.1**
构造DFA，接收{0，1}上的语言，字符串以0开头以1结尾
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111554395.png)

	该例题能体现出qt陷阱状态
**例3.2**
构造DFA，接收{0，1}上的语言，该语言的每个字符串不包含00子串（语言允许ε)。
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111558137.png)
	该例题能体现出有不止一个DFA来对应语言
**例3.3**
构造DFA，接收{0，1，2}上的语言，该语言的每个字符串代表的数字能整除3。
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111845690.png)
	该例题能体现出“状态”的意义
**例3.4**
构造DFA，接收{0，1}上的语言，该语言的每个字符串代表的二进制数能整除5。
分析：除以5的余数只能为0、1、2、3和4，使用如下5个状态分别代表已经读入数字的和除以5的不同余数的等价类。
q0：已经读入的数除以5，余数为0的输入串的等价类。q1：已经读入的数除以5，余数为1的输入串的等价类。q2：已经读入的数除以5，余数为2的输入串的等价类。q3：已经读入的数除以5，余数为3的输入串的等价类。94：已经读入的数除以5，余数为4的输入串的等价类。
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111847219.png)
	还是进一步体会状态的意义，因为是2进制，所以只需要给（原本余数2+input）%5

## NFA不确定有限状态自动机
- 至少有一条路径能接受串a时，可以理解为串a能被nfa接受
- DFA和NFA可以互相转换，是等价的，都接受正则语法
### 例题

**例3.5**
语言L={w|w∈a,b,c}\*且w中最后一个字母与第一个字母相同，|o|>1}。
(1)给出该语言的正则表达式：(2)构造NFA接收该语言：(3)将NFA转换为等价的DFA。
(1)a(a+b+c)a+b(a+b+c)"b+c(a+b+c)c
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111919869.png)
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111919503.png)

**例3.6**语言L={w|w∈{a,b}+且w中倒数第二个字母肯定在前面出现过}。

![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111923814.png)
**例3.7**
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111926055.png)

**例3.8**
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411111927039.png)

# 第四章 下推自动机
接受二型文法，特点是左比右少，左只有一个非终结符
对于串ω和下推自动机，从左到右对串进行扫描，下推自动机经过一系列动作后，如果最终栈存储器为空，则下推自动机能够接收串：下推自动机能够接收的所有串的集合，就是下推自动机接收的语言。
下推自动机在两种情况下停机：串扫描结束时或没有对应的下一步动作（此时，串还没有扫描结束)。停机时，有可能接收扫描过的串，也有可能不会接收扫描过的串（停机时，栈是否为空）。

#### 例题
**例4.1** 注意qf是双圈 finish的意思，然后因为这个是\*，所以可以有初始就是2然后迅速停机的方案
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411120124938.png) 
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411120124111.png)

**例4.2**
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411121529929.png)


![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411121529084.png)

# 第五章 图灵机
## 5.1 图灵机定义
### 例题

**例5.1** ab都只能拿#替换时，会多接受一些不该接受的，例如aababb
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411121921524.png)

**例5.2** ab分别用两种字符来替换
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411121932863.png)
**例5.3** ab串都是左边开始换
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411121940374.png)
**例5.4**开始前先检查
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122000518.png)
**例5.5**字母表有abc的时候
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122022747.png)
**例5.6**
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122023774.png)
## 5.2 图灵机非负整数计算

### 例题

**例5.7** 计算m+n 转化为B，m个0，1，n个0，B
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122123863.png)
**例5.8** 计算m - n 转化为{B，m个0，1，n个0，B} 减法值得注意的是左边会先透支一个0变B，所以要把中间的1转换为0，然后后面的1全换为B
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122134731.png)
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122134717.png)
## 5.3 图灵机构造技术
### 存储技术（x元组）

**例5.9** 状态当函数用
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122200086.png)
此外还有用上**二元组**的版本
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122213957.png)


### 移动技术

**例5.10** 状态当函数用

![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122344542.png)
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122351456.png)
### 扫描多个符号技术

**例5.11** 在下推自动机里最常见的题型
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411122356557.png)
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130007455.png)
**例5.12** 多元组的开头也可以视作flag-key，也就是说q是未找到101，而check时是已经找到一次了。
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130009068.png)
**例5.13**除了用状态存储以外，还可以一次性扫多字符（但这样做要求的行数会更多，不如状态吧）
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130019733.png)
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130019587.png)
### 多道技术

**例5.14** 非负二进制加法
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130106146.png)

**例5.15** 完全平方数
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130107417.png)
**例5.16** 斐波那契数列
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130108145.png)
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130109019.png)
**例5.17** 字符串子串
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130110172.png)
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130110792.png)
**例5.18**质数
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130111066.png)

### 查qi技术

**例5.19**查qi技术（借助多道纸带）在不修改原数据的前提下可以完成w和w的对比
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130057751.png)
### 子程序

![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130154811.png)
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130155993.png)
![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411130155616.png)

## 5.4其他图灵机

挺多的，大部分变种图灵机与基本图灵机等价，记住这个
## 5.5通用图灵机与编码

通用图灵机是能模拟所有图灵机的图灵机
编码如下：

![image.png](https://notepic-1327795028.cos.ap-chengdu.myqcloud.com/pic/202411131103967.png)
