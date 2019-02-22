# [腾讯精选练习](#腾讯精选练习)

| 章节 | 题目 |  解答 | 扩展 | 
| :--: | :-- | :-- | :--: |
| [**第一节 数组和字符串**](#数组和字符串) |  |   |  |
| -- | 1. 两数之和 | [1. 两数之和](#1) | 18 |
| -- | 15. 三数之和| [15. 三数之和](#15) | |
| -- | 16. 最接近的三数之和 | [16. 最接近的三数之和](#16) | |
| -- | 4. 寻找两个有序数组的中位数 | [4. 寻找两个有序数组的中位数](#4) | |
| -- | 5. 最长回文子串* | [5. 最长回文子串](#5) | |
| [**第二节 链表**](#链表) |  |  | |
| -- | 206. 反转链表 | [206. 反转链表](#206) | |
| -- | 2. 两数相加 | [2. 两数相加](#2) | 445 |
| -- | 21. 合并两个有序链表 | [21. 合并两个有序链表](#21) | |
| [**第三节 数学和数字**](#数学和数字) |  |  | |
| -- | 7. 整数反转 | [7. 整数反转](#7) |  |
| -- | 9. 回文数 | [9. 回文数](#9) | |
| -- | 136. 只出现一次的数字 | [136. 只出现一次的数字](#136) | |
| -- | 169. 求众数 | [169. 求众数](#169) | |
| -- | 231. 2的幂 | [231. 2的幂](#231) | |
| [**第四节 排序和搜索**](#排序和搜索) |  |  | |
| -- | 148. 排序链表 | [148. 排序链表](#148) |  |
| -- | 33. 搜索旋转排序数组 | [33. 搜索旋转排序数组](#33) | |
| --| 215. 数组中的第K个最大元素 | [215. 数组中的第K个最大元素](#215) | |
| -- | 230. 二叉搜索树中第K小的元素 | [230. 二叉搜索树中第K小的元素](#230) | |
| -- | 104. 二叉树的最大深度 | [104. 二叉树的最大深度](#104) | |
| -- | 124. 二叉树中的最大路径和 | [124. 二叉树中的最大路径和](#124) | |
| -- | 235. 二叉搜索树的最近公共祖先 | [235. 二叉搜索树的最近公共祖先](#235) | |
| -- | 236. 二叉树的最近公共祖先 | [236. 二叉树的最近公共祖先](#236) | |
| [**第五节 回溯算法**](#回溯算法) |  |  | |
| -- | 22. 括号生成 | [22. 括号生成](#22) | |
| -- | 78. 子集 | [78. 子集](#78) | |
| -- | 46. 全排列 | [46. 全排列](#46) | |
| -- | 89. 格雷编码 | [89. 格雷编码](#89) | |
| [**第六节 动态规划**](#动态规划) |  |  | |
| -- | 70. 爬楼梯 | [70. 爬楼梯](#70) |  |
| -- | 53. 最大子序和 | [53. 最大子序和](#53) | |
| -- | 121. 买卖股票的最佳时机 | [121. 买卖股票的最佳时机](#121) | |
| -- | 122. 买卖股票的最佳时机 II | [122. 买卖股票的最佳时机 II](#122) | |
| -- | 62. 不同路径 | [62. 不同路径](#62) | |
| [**第七节 设计**](#设计) |  |  |  |
| -- | 146. LRU缓存机制 | [146. LRU缓存机制](#146) | |
| -- | 155. 最小栈 | [155. 最小栈](#155) | |

# 腾讯精选练习

## 数组和字符串
### 1
[1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

```html
> 问题描述： 
给定一个整数数组 nums 和一个目标值 target，
请你在该数组中找出和为目标值的那两个整数，并返回他们的数组下标。
你可以假设每种输入只会对应一个答案。但是，你不能重复利用这个数组中同样的元素。

> 示例：
给定 nums = [2, 7, 11, 15], target = 9
因为 nums[0] + nums[1] = 2 + 7 = 9
所以返回 [0, 1]
```

```java
//思路：
//1、准备map,存储 <元素值，该元素在数组中的下标>
//2、对于任意一个 nums中元素 num，如果存在数组中找出和为target的另外一个整数，该整数值必然是(target-num)
public int[] twoSum(int[] nums, int target) {
    if(nums == null || nums.length <= 1){
        return null;
    }

    //<元素值，该元素在数组中的下标>
    Map<Integer,Integer> map = new HashMap<>();
    for(int index = 0;index < nums.length;index++){
        int num = nums[index];
        int v = target - num;
        if(map.containsKey(v)){ //map中包含v,说明 index 是结果数组中的元素
            return new int[]{index,map.get(v)};
        }
        map.put(num,index);
    }
    return null;
}
```

### 15
[15. 三数之和](https://leetcode-cn.com/problems/3sum/)
```html
> 问题描述：
给定一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，
使得 a + b + c = 0 ？找出所有满足条件且不重复的三元组。

注意：答案中不可以包含重复的三元组。

例如, 给定数组 nums = [-1, 0, 1, 2, -1, -4]，

满足要求的三元组集合为：
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

```java
//思路一：
//1、准备map，存储<值，该值在数组中出现的次数>
//2、如果该值 num 在数组中出现次数 >=3, num + num + num =0 ，则 num=0;返回一个解[0,0,0]
//3、如果该值 num 在数组中出现次数 >=2; num + num + num2 = 0,则需要判断 num2 (num2=-2 * num)是否在数组中，如果存在，返回 [num.num,num2]
//4、如果该值 num 在数组中出现次数 >=1; num + num2 + num3 = 0 ; 此时通过分别找出相应的 num2，所对应num3，如果有解，返回 [num,num2,num3]
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    if(nums.length < 3){
        return res;
    }

    //统计元素在数组中出现的次数
    Map<Integer,Integer> map = new HashMap<>();
    for(int num : nums){
        int freq = map.getOrDefault(num,0);
        map.put(num,++freq);
    }

    Set<Integer> set = map.keySet();

    for(Integer num : set){
        //num在数组中出现的频率
        int freq = map.get(num);

        //2、如果该值 num 在数组中出现次数 >=3, num + num + num =0 ，则 num=0;返回一个解[0,0,0]
        if(freq >= 3){
            if(num == 0){
                res.add(Arrays.asList(0,0,0));
            }
        }
        //3、如果该值 num 在数组中出现次数 >=2; num + num + num2 = 0,
        // 则需要判断 num2 (num2=-2 * num)是否在数组中，如果存在，返回 [num.num,num2]
        // (注意此时 num!=0,但是 num2可以等于0)
        if(freq >= 2){
            int num2 = 0 - 2 * num;
            if(map.containsKey(num2) && num!=0){
                res.add(Arrays.asList(num,num,num2));
            }
        }
        //4、如果该值 num 在数组中出现次数 >=1; num + num2 + num3 = 0 ;
        // 此时通过分别找出相应的 num2，所对应num3，如果有解，返回 [num,num2,num3]
        for(Integer num2 : set){
            int num3 = - num - num2;
            //假设 [num,num2,num3]是有序的并且num<num2<num3
            if(map.get(num3)==null || num>=num2 || num2>=num3){
                // map.get(num3)==null 表示的是在数组不存才该 num3元素，显然此时[num,num2,num3]不能作为解
                // num>=num2 || num2>=num3 防止出现 num、num2、num3相等的情况，这样会导致与前面的解重复
                continue;
            }
            res.add(Arrays.asList(num,num2,num3));
        }
    }
    return res;
}
```

```java
//思路二：
//1、num1 + num2 + num3 = 0,则 num1+num2 == -num3。实际上就是在数组查找 num1和num2,使得 num1 + num2 == -num3
//2、这样使得三数相加问题转化为两数相加问题
public List<List<Integer>> threeSum(int[] nums) {
    List<List<Integer>> res = new ArrayList<>();
    if(nums.length < 3){
        return res;
    }
    //这里进行排序，方便后面进行查找(我们使用的查找方式类似二分查找)
    Arrays.sort(nums);
    for(int i=0;i<nums.length-2;i++){
        if(i>0 && nums[i] == nums[i-1]){
            //我们这里要将 nums[i]作为 target值，
            // 对于相邻的相同元素，直接continue,可减少循环次数
            continue;
        }
        int target = - nums[i];
        int l = i+1,r = nums.length-1;
        //在[l,r]区间内查找和为 target的两个元素，
        //数组是有序的，在[0,l-1]区间内值都 <= nums[i],也就是说该区间内所有元素 >= target。显然找不到
        while(l<r){ //注意这里 l == r 是不行的 ，因为这样 nums[l],nums[r]就是同一元素了，不和题意
            if(nums[l]+nums[r] == target){
                res.add(Arrays.asList(nums[l],nums[r],-target));
                //TODO：去除重复元素
                while(l<r && nums[l] == nums[l+1]){
                    l++;
                }
                while(l<r && nums[r] == nums[r-1]){
                    r--;
                }
                l++;
                r--;
            }else if(nums[l]+nums[r] < target){
                l++;
            }else{ //nums[l]+nums[r] > target
                assert nums[l]+nums[r] > target;
                r--;
            }
        }
    }
    return res;
}
```

### 16
[16. 最接近的三数之和](https://leetcode-cn.com/problems/3sum-closest/)
```html
> 问题描述：

给定一个包括 n 个整数的数组 nums 和 一个目标值 target。
找出 nums 中的三个整数，使得它们的和与 target 最接近。返回这三个数的和。
假定每组输入只存在唯一答案。

例如，给定数组 nums = [-1，2，1，-4], 和 target = 1.

与 target 最接近的三个数的和为 2. (-1 + 2 + 1 = 2).
```

```java
//思路:参考15题的思路二
public int threeSumClosest(int[] nums, int target) {
    Arrays.sort(nums);

    int res = nums[0];
    //用于判断最接近的数字
    int coleset = Integer.MAX_VALUE;
    for(int i=0;i<nums.length-2;i++){
        int l = i+1;
        int r = nums.length-1;
        while(l<r){
            int num = nums[i] + nums[l] + nums[r];
            if(Math.abs(num - target) < coleset){ //num是教接近 target的元素
                coleset = Math.abs(num - target);
                res = num;
            }
            if(num < target){
                l++;
            }else if(num > target){
                r--;
            }else{ // num == target,此时直接返回 num即可
                return num;
            }
        }
    }

    return res;
}
```

### 4
[4. 寻找两个有序数组的中位数](https://leetcode-cn.com/problems/median-of-two-sorted-arrays/)

```html
> 问题描述：
给定两个大小为 m 和 n 的有序数组 nums1 和 nums2。
请你找出这两个有序数组的中位数，并且要求算法的时间复杂度为 O(log(m + n))。
你可以假设 nums1 和 nums2 不会同时为空。

> 示例：
示例 1:
nums1 = [1, 3]
nums2 = [2]
则中位数是 2.0

示例 2:
nums1 = [1, 2]
nums2 = [3, 4]
则中位数是 (2 + 3)/2 = 2.5
```

```java

```

### 5 
[5. 最长回文子串](https://leetcode-cn.com/problems/longest-palindromic-substring/)

```html
> 问题描述：
给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为 1000。

> 示例：
示例 1：
输入: "babad"
输出: "bab"
注意: "aba" 也是一个有效答案。

示例 2：
输入: "cbbd"
输出: "bb"
```

```java
//思路：
//1、考虑这是最长回文子串，回文串是对称的
//2、我们考虑从回文串的中间向两边扩展，这样来找最长的子回文串，算法复杂度为O(N^2)
//3、考虑两种情况：
// （1）像aba，这样长度为奇数。
// （2）想abba，这样长度为偶数。
public String longestPalindrome(String s) {
    if(s.length() <=1 ){ //只有一个字符，必然是回文串
        return s;
    }

    //最长回文串在s中的开始和结束位置,默认第一个字符是该最长回文串
    int startIndex = 0,endIndex = 0;
    int maxSubStrLen = 0 ;//最长子串长度

    //（1）像aba，这样长度为奇数。
    for(int i=1;i<s.length();i++){
        int l = i-1;
        int r = i+1;
        while((l>=0 && r<s.length()) && s.charAt(l) == s.charAt(r)){
            int tmpMaxSubStrLen = r-l+1;
            if(maxSubStrLen < tmpMaxSubStrLen){
                maxSubStrLen = tmpMaxSubStrLen;
                startIndex = l;
                endIndex = r;
            }
            l--;
            r++;
        }
    }

    //（2）想abba，这样长度为偶数。
    for(int i=0;i<s.length();i++){
        int l = i;
        int r= i+1;
        while((l>=0 && r<s.length()) && s.charAt(l) == s.charAt(r)){
            int tmpMaxSubStrLen = r-l+1;
            if(maxSubStrLen < tmpMaxSubStrLen){
                maxSubStrLen = tmpMaxSubStrLen;
                startIndex = l;
                endIndex = r;
            }
            l--;
            r++;
        }
    }
    //注意“左闭右开”
    return s.substring(startIndex,endIndex+1);
}
```

## 链表
### 206
[206. 反转链表](https://leetcode-cn.com/problems/reverse-linked-list/)
```html
> 问题描述：
反转一个单链表。

> 示例:

输入: 1->2->3->4->5->NULL
输出: 5->4->3->2->1->NULL
```

```java
public ListNode reverseList(ListNode head) {
    if(head==null){
        return null;
    }

    ListNode pre = null;
    ListNode cur = head;
    
    while(cur!=null){
        ListNode next = cur.next;
        
        //反转链表
        cur.next = pre;
        pre = cur;
        cur = next;
    }
    return pre;
}
```

### 2
[2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

```html
> 问题描述：
给出两个 非空 的链表用来表示两个非负的整数。
其中，它们各自的位数是按照 逆序 的方式存储的，并且它们的每个节点只能存储 一位 数字。

如果，我们将这两个数相加起来，则会返回一个新的链表来表示它们的和。

您可以假设除了数字 0 之外，这两个数都不会以 0 开头。

> 示例：

输入：(2 -> 4 -> 3) + (5 -> 6 -> 4)
输出：7 -> 0 -> 8
原因：342 + 465 = 807
```

```java
//思路：
//1、由于是逆序的，所以就直接按位相加即可
//2、注意处理进位问题
//3、有可能要增加节点，比如 9+9 = 18,就需要要原来的基础上再加节点
//注意：新增节点的情况
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    if(l1 == null){
        return l2;
    }
    if(l2 == null){
        return l1;
    }

    ListNode dummyHead = new ListNode(-1);
    ListNode tail = dummyHead;

    //digit表示每位上按位相加后的值,有可能大于10
    int digit = 0;
    ListNode cur1 = l1;
    ListNode cur2 = l2;
    //注意要考虑这两个链表有可能是不等长的。
    while(cur1!=null || cur2!=null){
        if(cur1 != null){
            digit += cur1.val;
            cur1 = cur1.next;
        }
        if(cur2 != null){
            digit += cur2.val;
            cur2 = cur2.next;
        }
        //创建新节点，将该新节点插入到新链表中
        ListNode node = new ListNode(digit%10);
        tail.next = node;
        tail = node;
        digit /= 10;
    }
    //类似 9+9 =18的情况
    if(digit == 1){
        ListNode node = new ListNode(1);
        tail.next = node;
        tail = node;
    }
    //TODO：注意尾插法，最后一个元素的处理
    tail.next = null;
    return dummyHead.next;
}
```

### 21
[21. 合并两个有序链表](https://leetcode-cn.com/problems/merge-two-sorted-lists/)

```html
> 问题描述：
将两个有序链表合并为一个新的有序链表并返回。新链表是通过拼接给定的两个链表的所有节点组成的。 

> 示例：

输入：1->2->4, 1->3->4
输出：1->1->2->3->4->4
```

```java
//思路：类似合并两个有序数组
public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
    if(l1 == null){
        return l2;
    }
    if(l2 == null){
        return l1;
    }

    ListNode dummyHead = new ListNode(-1);
    ListNode tail = dummyHead;

    while(l1!=null && l2!=null){
        if(l1.val < l2.val){
            //链表l1当前节点值较小，加入到新链表中
            tail.next = l1;
            tail = l1;
            l1 = l1.next;
        }else{
            tail.next = l2;
            tail = l2;
            l2 = l2.next;
        }
    }

    //注意:这两种情况要么智执行其中一种、要么都不执行
    if(l1 != null){
        tail.next = l1;
    }
    if(l2 != null){
        tail.next = l2;
    }
    //TODO:这里的尾插法,tail.next =null，是不需要的，
    //因为tail不一定指向链表最后一个元素；tail仅仅是指向我们遍历两个链表的最后一个元素
    return dummyHead.next;
}
```


## 数学和数字
### 7
[7. 整数反转](https://leetcode-cn.com/problems/reverse-integer/)

```html
> 问题描述：

给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。

> 示例：

示例 1:
输入: 123
输出: 321

示例 2:
输入: -123
输出: -321

示例 3:
输入: 120
输出: 21
```

```java
//思路：
// 1、reverseX记录倒置后的数字
// 2、 注意这里会发生发生溢出问题，比如 1534236469，倒置后数据就不在 int类型的范围内了
public int reverse(int x) {
    //记录倒置后的整数
    long reverseX = 0;
    while(x!=0){
        reverseX = reverseX * 10 + x%10;
        x/=10;
    }
    if(reverseX < Integer.MIN_VALUE || reverseX > Integer.MAX_VALUE ) {
        return 0;
    }
    return (int) reverseX;
}
```

### 9
[9. 回文数](https://leetcode-cn.com/problems/palindrome-number/)
```html
> 问题描述：

判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数。

> 示例：

示例 1:
输入: 121
输出: true

示例 2:
输入: -121
输出: false
解释: 从左向右读, 为 -121 。 从右向左读, 为 121- 。因此它不是一个回文数。

示例 3:
输入: 10
输出: false
解释: 从右向左读, 为 01 。因此它不是一个回文数。
```

```java
//思路：与第7题思路类似
public boolean isPalindrome(int x) {
    if(x<0){
        return false;
    }
    int reverseX = 0;
    int num = x;
    while(num!=0){
        reverseX = reverseX*10 + num%10;
        num/=10;
    }
    return reverseX == x;
}
```

### 136
[136. 只出现一次的数字](https://leetcode-cn.com/problems/single-number/)

### 169
[169. 求众数](https://leetcode-cn.com/problems/majority-element/)

### 231
[231. 2的幂](https://leetcode-cn.com/problems/power-of-two/)

## 排序和搜索

### 148
[148. 排序链表](https://leetcode-cn.com/problems/sort-list/)

### 33
[33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

### 215
[215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

### 230
[230. 二叉搜索树中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)

### 104
[104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

### 124
[124. 二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

### 235
[235. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

### 236
[236. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

## 回溯算法
### 22
[22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

### 78
[78. 子集](https://leetcode-cn.com/problems/subsets/)

### 46
[46. 全排列](https://leetcode-cn.com/problems/permutations/)

### 89
[89. 格雷编码](https://leetcode-cn.com/problems/gray-code/)

## 动态规划
### 70
[70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

### 53
[53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

### 121
[121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

### 122
[122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

### 62
[62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)

## 设计 
### 146
[146. LRU缓存机制](https://leetcode-cn.com/problems/lru-cache/)

### 155
[155. 最小栈](https://leetcode-cn.com/problems/min-stack/)
