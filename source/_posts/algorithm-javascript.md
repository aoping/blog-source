---
title: 算法
date: 2017-10-18 14:41:26
tags: algorithm javascript
categories: 学习笔记
---

javascript实现算法

<!--more-->

### 二分查找
需求：在一个有序数组a中查找一个数n
算法：取中间键mid，比较a[mid]和n，n大就继续在右边查找，n小就在左边查找



## 排序

### 桶排序

#### 场景： 已知元素要求可以枚举
#### 算法： 初始化好空桶（值为0），再遍历数组数值放到对应的桶
#### javascript实现
```javascript
function sort(a) {
  let arry = []
  for(let i =0; i<11;i++) {
    arry[i] =0
  }
  for(let i= 0;i<a.length;i++) {
    arry[a[i]]++
  }
  for(let i= 0;i<11;i++) {
    if(arry[i]!==0) {
    for(let j= 0;j<arry[i];j++) {
      console.log(i)
    }
    }
  }
}

sort([5,3,5,2,8])

```
#### 算法时间复杂度 O(M+N) m是桶的数量，n是要排序的数组大小
#### 优缺点
- 优点：快
- 缺点： 浪费空间


### 冒泡排序
#### 算法：每次比较两个相邻的元素，如果顺序错了就交换位置(第一次遍历：比较第1、2位，再比较2、3位，至n位，第二次遍历比较第1、2位，再比较2、3位，至n-1位,...此过程中遍历几次，最后几位就是排好序的)

#### javascript实现
```javascript
function sort(a){
  for(let i=0;i<a.length;i++){
    for(let j=0;j<a.length-i-1;j++){
      if(a[j]<a[j+1]) {
      let tmp = a[j]
      a[j] = a[j+1]
      a[j+1] = tmp
      }
    }
  }
  console.log(a)
}

sort([5,3,5,2,8])
```
#### 算法时间复杂度 O(n*2)，一般不用
#### 优缺点
- 缺点： 慢
- 优点： 节约空间（相对于桶排序）

### 快速排序
#### 算法：一个数组a,先随便找一个基准数,一般设start=0第一个设为k=a[start]，然后i从左到右查找第一个大于k的数a[i]，j从右到左找第一个小于k的数a[j]，如果i不大于j则交换两个数字继续遍历，遍历结束交换a[start]和a[j],这样位置j左边的都小于k,右边都大于k
接着位置j左右两边继续上诉操作

#### javascript实现
```javascript


```

在不同情况下使用不同的算法

### 计数排序 基数排序 插入排序 归并排序 堆排序


## 队列 栈 链表

### 队列

队列有三个基本元素： 一个数组 一个头 一个尾
```
struct queue {
  let data[100]; // 队列主体
  let head; // 队首
  let tail; // 队尾

}
```

### 栈
#### 运用
- 判断是否是回文字符




