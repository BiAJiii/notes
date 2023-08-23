# LeetCode（Updating…）

## 2、两数相加（考核链式）

给你两个 **非空** 的链表，表示两个非负的整数。它们每位数字都是按照 **逆序** 的方式存储的，并且每个节点只能存储 **一位** 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。



__思路__：由于JS中没有内置链表，这里是自定义好的链式。其工作原理为，定义值val和next指向，而next会指向下一个node的val（对象套对象）。

1、判断l1和l2是否为其链式最后一位数，如果都是，跳出循环。注意：这里的l1和l2都是对象，所以即便他们都是空的，也不会跳出循环。所以，只有他们都为null，即为链式的结尾时，才会跳出while循环。

2、将l1和l2的node的val处理，赋给l3的node

3、l1和l2转跳到下一个node

4、当跳出循环，表示l1和l2都已经到尾部，这时判断是否有进位，有的话给l3再添加一个进位即可

5、注意：l3 new完后赋值给a3（不要对原链进行操作），这样l3可以作为链式的头部，如果直接用l3进行所有操作，最后返回l3的时候，只有链式的最后一个位或倒数第二位（有进位的情况）。

```
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */
 //这里自定义的链式，next都指向下一个node的val
var addTwoNumbers = function(l1, l2) {
    let a1 = l1
    let a2 = l2
    let carry = 0
    let l3 = new ListNode()
    let a3 = l3
    //如果a1和a2中有一个没有读到null（结尾），循环继续。
    while(a1 || a2){
        //如果a1先结束，给后面的值都赋为0
        const val1 = a1?a1.val:0;
        //a2同理
        const val2 = a2?a2.val:0;
        const val3 = (val1 + val2 + carry) % 10
        //判断是否有进位
        carry = Math.floor((val1 + val2 + carry) / 10)

        a3.next = new ListNode(val3)
        //判断a是否为结尾，不是的话，读下一个node
        if(a1) {a1 = a1.next}
        if(a2) {a2 = a2.next}
        a3 = a3.next
    }
    //判断最后一位是否有进位
    if(carry === 1){
        a3.next = new ListNode(carry)
    }
    return l3.next
};


```

补充上面第五点：

* 情况一

```
let a = new ListNode();
// let b = a
a.next = new ListNode(1)
a = a.next
a.next = new ListNode(2)
a = a.next
console.log(a)
```

结果：![image-20230111163621543](https://raw.githubusercontent.com/BiAJiii/imgsBed/main/imgs/202301111636119.png)

很明显，其实上面的代码只是不断更新a这个对象中的next属性，将最后new出来的ListNode(2)又赋给了a，最后a还是只有一个node



* 情况二

```
let a = new ListNode();
let b = a
//此时，b===a
b.next = new ListNode(1)
b = b.next
//b已经是一个全新的对象（即next指向的下一个node）， b!==a
b.next = new ListNode(2)
b = b.next
console.log(a)
```

结果：![image-20230111163956390](https://raw.githubusercontent.com/BiAJiii/imgsBed/main/imgs/202301111639562.png)

可以看出，这里没有直接修改链式a的属性，而是给a.next嵌套了一个新的node对象。





## 3、无重复字符的最长字串

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

```
例子1：
输入: s = "abcabcbb"
输出: 3 
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
例子2：
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

这道题想的挺久的，一开始是下面的思路（其实是读题没读对），后面才发现想的方向错了。下面的代码其实是解决一个字符串中，首尾元素重复的子字符串的最大或最小长度。

```
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    let arr = Array.from(s)
    let len = arr.length
    let maxCount = 0
    for(let i = 0; i < len - 1; i++){
        let j = i + 1
        let count = 0

        while(1){
            count++
            if(arr[i] == arr[j]) {
                break
            }
            if(count > maxCount) {
                maxCount = count
            }

            j++
            if(j == len) {
                break
            }

        }
    }
    return maxCount
}
```

后来实在想不到了，就看到下面这幅图，思想很清晰，具体实现过程写在代码的注释里了。

![img](https://raw.githubusercontent.com/BiAJiii/imgsBed/main/imgs/202301121417343.png)

```
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    //先将字符串转数组
    let arr = Array.from(s)
    //将该数组的第一位赋给新数组[]
    let newArr = [arr[0]]
    let len = arr.length
    let newLen = newArr.length
    let maxCount = 0
    //对数组arr进行遍历
    for(let i = 1; i < len; i++){
        //在arr的基础上对newArr进行遍历
        for(let j = 0; j < newLen; j++){
            //判断是否新数组中是否已经存在 属于arr下标i对应的元素
            let index = newArr.indexOf(arr[i])
            newArr.push(arr[i])
            //存在的话（newArr中相同的元素最多有两个，且其他元素皆无相同元素），
            //将找到相同元素的第一个元素前面的全部数组删除。
            if(index >= 0){
                newArr.splice(0 , index + 1)
            }
            //如果修改后的数组长度要大于前面记录的maxCount，赋值
            if(newArr.length > maxCount){
                maxCount = newArr.length
            }
        }
    }
    return maxCount
}
```



## 5、最长回文串

给你一个字符串 `s`，找到 `s` 中最长的回文子串。

如果字符串的反序与原始字符串相同，则该字符串称为回文字符串。

 ```
 例子：
 输入：s = "babad"
 输出："bab"
 解释："aba" 同样是符合题意的答案。
 ```

又是想了很久的题目，思路是左右指针偏移的情况。

![截屏2019-12-06上午7.54.28.png](https://pic.leetcode-cn.com/533a8538f42e6a6495b87d0c054224fdaa2e6da1cd9158f3e9042894137961fc-截屏2019-12-06上午7.54.28.png)

本以为是很简单的情况，但越写发现情况越多，虽然最后代码写出来了，但实在是太复杂了。。。

```
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
    let arr = Array.from(s)
    let len = arr.length
    let OutArr = [arr[0]]
    //数组长度小于三的情况
    if(arr.length <= 2){
        if(arr[0]==arr[1]){
            return s
        } else {
            return arr[0]
        }
    }

    //数组长度大于等于三的情况
   for(let i = 1; i < (len - 1); i++){
        let j = (i - 1)//左指针
        let k = (i + 1)//右指针
        //如果一开始左指针和i相同，就让左指针一直左移，直到不同；
        while((arr[j] == arr[i])){
            //跳出循环两个条件
            //1、左指针到达尽头
            //2、左指针的数不等于右指针的数（这种情况是为了解决左右指针一开始就不同的字符串 如 1223 12224）
            if(arr[k] != arr[j] && (k-j) >= OutArr.length){
                OutArr = arr.slice(j,k)
                break
            }
            if(j == 0) break
            if(j > 0){
                j--//左指针左移
            }
        }
        while((arr[k] == arr[i])){
            //这边和上面是同理的
            if( arr[k] != arr[j]){
                //(k-j) >= OutArr.length是为了保证最后一轮进入不了判断3，而影响OutArr结果
                if(arr[j]==arr[i] && (k-j) >= OutArr.length){
                    OutArr = arr.slice(j , k+1)
                }
                if(arr[j] != arr[i] && (k-j) >= OutArr.length){
                    OutArr = arr.slice(j+1 , k+1)
                }
                k++
                break
            }
            if(k == (len - 1)) break
            if(k < len){
                k++//右指针右移
            }
        }

        //判断3：进入开始判断左右指针(此时左右指针之间的数字为一个或多个arr[i]，即(左指针)11111(右指针))
        while(arr[k] == arr[j]){
            //左右指针相同，就继续扩大范围
            if(arr[k] == arr[j]){
               let tempArr = arr.slice(j, (k + 1))
               //判断这次循环的回文字符串是否是最大的
               if(tempArr.length >= OutArr.length) {
                    OutArr = tempArr
                }
                //如果左右指针在不断移动的过程中仍相同，当左指针或右指针到尽头，跳出来
                if(j == 0 || k == (len + 1)){
                    break
                }
            }
            j--
            k++
        }
   }

   return OutArr.join('')
};

```

别人写的，思路一样，这个其实就是将情况分成了两种，奇数长度（aba）和偶数长度（abba）：

```
/**
 * @param {string} s
 * @return {string}
 */
var longestPalindrome = function(s) {
        if (s.length<2){
            return s
        }
        let res = ''
        for (let i = 0; i < s.length; i++) {
            // 回文子串长度是奇数
            helper(i, i)
            // 回文子串长度是偶数
            helper(i, i + 1) 
        }

        function helper(m, n) {
            while (m >= 0 && n < s.length && s[m] == s[n]) {
                m--
                n++
            }
            // 注意此处m,n的值循环完后  是恰好不满足循环条件的时刻
            // 此时m到n的距离为n-m+1，但是mn两个边界不能取 所以应该取m+1到n-1的区间  长度是n-m-1
            if (n - m - 1 > res.length) {
                // slice也要取[m+1,n-1]这个区间 
                res = s.slice(m + 1, n)
            }
        }
        return res
};

作者：Salvatore
链接：https://leetcode.cn/problems/longest-palindromic-substring/solutions/697935/chao-jian-dan-de-zhong-xin-kuo-san-fa-yi-qini/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



## 35、搜索插入位置

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

请必须使用时间复杂度为 `O(log n)` 的算法。

> ```
> 实例一：
> 输入: nums = [1,3,5,6], target = 5
> 输出: 2
> 实例二：
> 输入: nums = [1,3,5,6], target = 2
> 输出: 1
> 实例三：
> 输入: nums = [1,3,5,6], target = 7
> 输出: 4
> ```

这道题其实很好想到使用二分法做，但写的时候还是遇到很多问题，其实就是边界定义搞不清楚。

用了很多if去限制边界，这样其实是很麻烦的。

> ```
> /**
>  * @param {number[]} nums
>  * @param {number} target
>  * @return {number}
>  */
> var searchInsert = function(nums, target) {
>     let min = 0
>     let max = nums.length - 1
>     let index
>     let out = nums.length
>     while(min <= max) {
>         //取中间索引，使用以下方法而不是Math.floor((max + min) /2)，是防止溢出
>         index = min + Math.floor((max - min) /2)
>         //如果目标值比中间索引对应的值大，让最小值向中间索引右边移动一位，
>         //因为跳出循环条件是最大值小于最小值
>         //所以当目标值>中间索引对应的值时，target对应的索引必然不是此时index，且必然会进入下一次循环
>         //而当目标值<或=中间索引对应的值时,target对应的索引可能是此时index，所以需要用out记录此index
>         if(target > nums[index]){
>             min = index + 1
>         } else {
>             out = index
>             max = index - 1
>         }
>     }
>     return out
> };
> ```



## 69、x的平方根

给你一个非负整数 `x` ，计算并返回 `x` 的 **算术平方根** 。

由于返回类型是整数，结果只保留 **整数部分** ，小数部分将被 **舍去 。**

**注意：**不允许使用任何内置指数函数和算符，例如 `pow(x, 0.5)` 或者 `x ** 0.5` 。

 

* 牛顿迭代法

![image-20230131154010954](https://raw.githubusercontent.com/BiAJiii/imgsBed/main/imgs/202301311540205.png)

由于是求平方根

即是`y = x^2 - C`，选择x0=C为初始值

其中C就是y=0时候，开方对应的要求得的值即：C=x^2 =>  x = C^1/2 （x为最终求得的平方根，C为要计算的平方根），其中切点为（x0，x0^2 - C）

可以得到切线函数为 `y - (x0^2 + C) = 2x0(x - x0)  `

使 y=0 可以得到新的与x轴相交的切线的点 x1

`x = 1/2(x0 + C/x0)` 

将x赋给x0，这样子，x就会不断迭代，向着真正的根x逼近。

由于JS中数字是有精度的，当x0无限接近x的时候，x^2也无限接近于C，当精度到达一定数量级，x^2 == C

> ```
> /**
>  * @param {number} x
>  * @return {number}
>  */
> var mySqrt = function(x) {
>     let c = x
>     let x0 = x
>     while(x0*x0 > x){
>         x0 = 0.5*(x0 + c/x0) | 0
>     }
>     return Math.floor(x0)
> };
> ```



## 70、爬楼梯


假设你正在爬楼梯。需要 `n` 阶你才能到达楼顶。

每次你可以爬 `1` 或 `2` 个台阶。你有多少种不同的方法可以爬到楼顶呢？



* 斐波那契数列

​		其实这道题，可以倒着想。当在第n层的时候有f(n)种方法到达第n层，那么要想达到第n层，就只有从第n-1层爬一阶或者第n-2层爬两阶两种方法。

​		那么第n-1层=>f(n-1)种方法到第n-1层；同理第n-2层=>f(n-2)种方法到第n-2层；

​		这也就可以推算出，f(n) = f(n-1) + f(n+2) 然后可以递归回到第1、2层

​		到达第一层只有一种方法:f(1)=1，到达第二层有两种方法f(2)=2，这样倒退就可以得到f(n)了。

> ```
> /**
>  * @param {number} n
>  * @return {number}
>  */
> var climbStairs = function(n) {
>     let arr = new Array(n).fill(0)
>     arr[0] = 1
>     arr[1] = 1
>     for(let i = 2 ; i <= n ; i++){
>         arr[i] = arr[i-1] + arr[i-2]
>     }
>     return arr[n]
> 
> };
> ```
