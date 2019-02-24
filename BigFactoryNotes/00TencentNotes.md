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
| -- | 169. 求众数* | [169. 求众数](#169) |  229 |
| -- | 231. 2的幂 | [231. 2的幂](#231) | |
| [**第四节 排序和搜索**](#排序和搜索) |  |  | |
| -- | 148. 排序链表 | [148. 排序链表](#148) |  |
| -- | 33. 搜索旋转排序数组 | [33. 搜索旋转排序数组](#33) | |
| -- | 215. 数组中的第K个最大元素 | [215. 数组中的第K个最大元素](#215) | |
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
//思路一：直接合并然后求解，但是不合题意。
//时间复杂度：O(m+n)
//空间复杂度：O(m+n)
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int len = nums1.length + nums2.length;
    int[] nums = new int[len];
    int index = 0;
    int i = 0;
    int j = 0;
    while(i<nums1.length && j< nums2.length){
        if(nums1[i] < nums2[j]){
            nums[index++] = nums1[i++];
        }else{
            nums[index++] = nums2[j++];
        }
    }
    while(i< nums1.length){
        nums[index++] = nums1[i++];
    }
    while(j< nums2.length){
        nums[index++] = nums2[j++];
    }
    if(len % 2 ==1){
        return nums[nums.length/2]*1.0;
    }else{
        return (nums[nums.length/2] + nums[nums.length/2-1])*1.0 / 2;
    }
}
```

```java
//思路二：
//1、要求时间复杂度 O(log(m+n)),m+n就是两个数组的长度和，又是有序数组，我们很容易想到二分查找
//2、求出的结果是中位数，中位数的特点是其以后的数都比它大，前面的数都比它小。
//3、两个数组都已经是有序数组，
// 因此我们所需要的结果就是num1[start1,end1]中的第i个元素(下标 start1+i-1)和数组num2[start2,end2]中第j个元素(下标 start+j-1)，
///在数组num1[start1,end1]中确定i以及在数组中确定num2[start2,end2]，此时可以采用二分查找的方法，
// 通过不断缩小查找范围来确实所需要查找的值，也符合题目中所要求的分治算法的思想。
public double findMedianSortedArrays(int[] nums1, int[] nums2) {
    int len1 = nums1.length;
    int len2 = nums2.length;
    int k1 = (len1+len2+1)/2;
    int k2 = (len1+len2+2)/2;
    //当 (len1+len2)奇数时，此时 k1==k2;
    //当 (len1+len2)偶数时，此时 k1+1 == k2
    double res =
            (findKth(nums1,0,len1-1,nums2,0,len2-1,k1) +
                    findKth(nums1,0,len1-1,nums2,0,len2-1,k2))/2;
    return res;
}

/**
 * 查找 nums1[start1,end1] 和 nums2[start2,end2]合并后的第 k 小元素
 */
private double findKth(int[] nums1, int start1, int end1, int[] nums2, int start2, int end2, int k) {
    //计算当前数组范围内的数组长度
    int len1 = end1 - start1 + 1;
    int len2 = end2 - start2 + 1;
    if(len1 > len2){
        //这里保持 len1 <= len2,方便后面的操作
        return findKth(nums2,start2,end2,nums1,start1,end1,k);
    }else if(len1 == 0){
        //nums1[start1,start2]数组长度为0，则就是在nums2[start2,end2]中第 k 小的元素
        return nums2[start2+k-1];
    }else if(k == 1){
        //合并后的数组的第1个元素，显然是nums1[start1,end1]和nums2[start2,end2]中第一个元素的较小值
        return Math.min(nums1[start1],nums2[start2]);
    }
    //分治
    int i = Math.min(k/2,len1); //在nums1[start1,end1]中第 i 小元素
    int j = k - i; //在nums2[start2,end2]中第 j 小元素
    if(nums1[start1+i-1] > nums2[start2+j-1]){  //此时 nums2[start2,end2]中就要舍弃前面j个元素
        /**
         * 使用反证法证明：
         * 证：当k/2 >= len1 时，而我们要找的k就在nums2[start2,end2]的前 k/2元素中。
         * 我们假设 k 所在的数组下标记为p，那么nums2[start2,end2]中含有的属于后数组前k个元素的元素有(p+1)个。
         * 显然，nums1[start1,end1]中必然含有另外 k-(p+1)个元素。
         * 由此，得到如下不等式：
         * p <= k/2 - 1 （k th 实际所处位置为p，在nums2[start2,end2]的前k/2个元素里。-1是因为现在算的是数组下标，从0开始）
         * ==> p + 1 <= k/2；
         * ==> k - (p+1) >= k - k/2。
         显然，len1 >= k - (p+1) >= k/2 ，这与上面的假设，k/2 >= len1是矛盾的。
         */
        return findKth(nums1,start1,end1,nums2,start2+j,end2,k-j);  //此时就是求第(k-j)小元素
    }else if(nums1[start1+i-1] < nums2[start2+j-1]){ //此时 nums1[start1,end1]中就要舍弃前面i个元素
        return findKth(nums1,start1+i,end1,nums2,start2,end2,k-i);
    }else{
        return nums1[start1+i-1];
    }
}
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

```html
> 问题描述：
给定一个非空整数数组，除了某个元素只出现一次以外，其余每个元素均出现两次。
找出那个只出现了一次的元素。

说明：
你的算法应该具有线性时间复杂度。 你可以不使用额外空间来实现吗？

> 示例：
示例 1:
输入: [2,2,1]
输出: 1

示例 2:
输入: [4,1,2,1,2]
输出: 4
```

```java
//思路：利用异或运算的性质 : 如果两个相同元素异或，所得结果为0 ; 0 与任何整数异或，该整数值不变
//1、对整个数组元素进行异或运算
//2、异或运算的结果即为所求
public int singleNumber(int[] nums) {
    int ret=0;
    for(int i=0;i<nums.length;i++){
        ret^=nums[i];
    }
    return ret;
}
```

### 169
[169. 求众数](https://leetcode-cn.com/problems/majority-element/)

```html
> 问题描述：
给定一个大小为 n 的数组，找到其中的众数。众数是指在数组中出现次数大于 ⌊ n/2 ⌋ 的元素。

你可以假设数组是非空的，并且给定的数组总是存在众数。

> 示例：
示例 1:
输入: [3,2,3]
输出: 3

示例 2:
输入: [2,2,1,1,1,2,2]
输出: 2
```

> 背景知识：摩尔投票算法
摩尔投票法基于以下定理，找到数组中超过一半的数。
定理：
如果一个数组里存在**一个数超过一半**，那么同时删去两个不同的数，超过一半的数仍然超过一半。
推广-1：
如果一个数组里有一元素超过1/3，那么同时删除3个不同的数，超过1/3的数仍然超过1/3。
推广-2：
如果一个数组里有一元素超过1/k, 那么同时删除k个不同的数，超过1/k的数仍然超过1/k。

```java
//思路：典型的摩尔投票算法
//如果删去的两个数有一个是超过一半的：
//假设每次都删除一个超过一半的，一个不超过一半的，那么一定是不超过一半的数先被删完。
public int majorityElement(int[] nums) {
    int majority = nums[0];
    int count = 0; //统计主元素数目
    for(int num : nums){
        if(count ==0){
            //说明之前假定的主元素并不是主元素 1 1 1 2 2 2 6 6 6 6 6 6 6
            majority = num;
            count = 1;
        }else if(majority == num){
            count++;
        }else{
            count--;
        }
    }

    //归0操作，用来统计主元素出现次数
    count = 0;
    for(int num : nums){
        if(num == majority){
            count++;
        }
    }
    if(count > nums.length/2){
        return majority;
    return -1;
}
```

### 229
> [229. 求众数 II](https://leetcode-cn.com/problems/majority-element-ii/)

```html
> 问题描述：
给定一个大小为 n 的数组，找出其中所有出现超过 ⌊ n/3 ⌋ 次的元素。

说明: 要求算法的时间复杂度为 O(n)，空间复杂度为 O(1)。

> 示例：
示例 1:
输入: [3,2,3]
输出: [3]

示例 2:
输入: [1,1,1,3,3,2,2,2]
输出: [1,2]
```

//思路：
//1、该数组中最多只有2个元素个数超过 1/3 num.length
//2、仍然采用摩尔投票算法
public List<Integer> majorityElement(int[] nums) {
    List<Integer> res = new ArrayList<>();
    if(nums.length == 0){
        return res;
    }
    int num1 = nums[0];
    int num2 = -nums[0];
    int count1 = 0;
    int count2 = 0;
    for(int num : nums){
        if(num == num1){
            count1++;
        }else if(num == num2){
            count2++;
        }else if(count1==0){
            num1 = num;
            count1 = 1;
        }else if(count2==0){
            num2 = num;
            count2 =1;
        }else{
            count1--;
            count2--;
        }
    }

    count1 = 0;
    count2 = 0;
    for(int num : nums){
        if(num == num1){
            count1++;
        }else if(num == num2){
            count2++;
        }
    }
    if(count1 > nums.length/3){
        res.add(num1);
    }
    if(count2 > nums.length/3){
        res.add(num2);
    }
    return res;
}
```

### 231
[231. 2的幂](https://leetcode-cn.com/problems/power-of-two/)

```html
> 问题描述：
给定一个整数，编写一个函数来判断它是否是 2 的幂次方。

> 示例：
示例 1:
输入: 1
输出: true
解释: 2^0 = 1

示例 2:
输入: 16
输出: true
解释: 2^4 = 16

示例 3:
输入: 218
输出: false
```
```java
//思路一：
// 1、显然，这里的 n 肯定是正整数
// 2、n 使用二进制表示，如果是2的幂次方，则二进制中 1 只出现1次。
public boolean isPowerOfTwo(int n) {
    if(n <= 0){
        return false;
    }
    int count = 0;
    for(int i=0;i<32;i++){
        int bit = (n&1);
        if(bit==1){
            count++;
        }
        n >>= 1;
    }
    return count == 1;
}
```

```java
//思路二：
//1、位运算，2的次幂的二进制表示中，最高位为1，其余位均为0；
//例如：n=4（100），n-1=3(011), 将n和n-1做"与运算"结果为0，
//2、通过这个性质来判断一个数是否为2的次幂，即可。
public boolean isPowerOfTwo(int n) {
    if (n <= 0) {
        return false;
    }
    return (n&(n-1)) == 0;
}
```

## 排序和搜索

### 148
[148. 排序链表](https://leetcode-cn.com/problems/sort-list/)

```html
> 问题描述：
在 O(n log n) 时间复杂度和常数级空间复杂度下，对链表进行排序。

> 示例：
示例 1:
输入: 4->2->1->3
输出: 1->2->3->4

示例 2:
输入: -1->5->3->4->0
输出: -1->0->3->4->5
```

```java
//思路：
//1、时间复杂度在 O(n logn)的排序算法，有归并排序、快速排序、堆排序。这里使用归并排序
//2、注意：链表为空或者链表只有一个元素是不需要排序的
//3、我们这里归并排序，涉及到递归调用，注意递归结束条件
public ListNode sortList(ListNode head) {
    if(head == null || head.next ==null){
        return head;
    }
    ListNode head2 = getMidNode(head);
    return merge(sortList(head),sortList(head2));
}

//获取该链表的中间节点(其实是获取以该中间节点为头结点的链表)
private ListNode getMidNode(ListNode head){
    //pre指向目标节点的前一个节点
    ListNode pre = head;
    ListNode slow = head;
    ListNode fast = head;
    while(slow !=null && fast != null){
        pre = slow;
        slow = slow.next;
        fast = fast.next;
        if(fast!=null){
            fast = fast.next;
        }else{
            break;
        }
    }
    pre.next = null;
    //此时 slow 指向该链表的中间节点
    ListNode head2 = slow;
    return head2;
}

//合并两个有序链表(类比合并两个有序数组)
private ListNode merge(ListNode head1,ListNode head2){
    ListNode dummyHead = new ListNode(-1);

    if(head1 == null){
        return head2;
    }
    if(head2 == null){
        return  head1;
    }
    ListNode tail = dummyHead;
    while(head1 !=null && head2 != null){
        if(head1.val < head2.val){
            tail.next = head1;
            tail = head1;
            head1 = head1.next;
        }else{
            tail.next = head2;
            tail = head2;
            head2 = head2.next;
        }
    }
    if(head1 !=null){
        tail.next = head1;
    }
    if(head2 !=null){
        tail.next = head2;
    }
    return dummyHead.next;
}
```

### 33
[33. 搜索旋转排序数组](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)

```html
> 问题描述:
假设按照升序排序的数组在预先未知的某个点上进行了旋转。
( 例如，数组 [0,1,2,4,5,6,7] 可能变为 [4,5,6,7,0,1,2] )。
搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回 -1 。
你可以假设数组中不存在重复的元素。
你的算法时间复杂度必须是 O(log n) 级别。

> 示例：
示例 1:

输入: nums = [4,5,6,7,0,1,2], target = 0
输出: 4
示例 2:

输入: nums = [4,5,6,7,0,1,2], target = 3
输出: -1
```
```java
//思路：
// 1、对于数组[0 1 2 4 5 6 7] 共有下列七种旋转方法：
//[0 1 2 {3} 4 5 6 7]
//[7 0 1 {2} 3 4 5 6]
//[6 7 0 {1} 2 3 4 5]
//[5 6 7 {0} 1 2 3 4]
//[4 5 6 {7} 0 1 2 3]
//[3 4 5 {6} 7 0 1 2]
//[2 3 4 {5} 6 7 0 1]
//[1 2 3 {4} 5 6 7 0]
//2、二分搜索法的关键在于获得了中间数后，判断下面要搜索左半段还是右半段，
// 如果中间的数小于最右边的数，则右半段是有序的，
// 如果中间数大于最右边数，则左半段是有序的，
//3、我们只要在有序的半段里用首尾两个数组来判断目标值是否在这一区域内。
public int search(int[] nums, int target) {
    int lo = 0;
    int hi = nums.length -1;
    while(lo<=hi){
        int mid = (hi - lo)/2 + lo;
        if(nums[mid]==target){
            return mid;
        }else if(nums[mid]<nums[hi]){  //右半段是有序的
            if(target > nums[mid] && target <= nums[hi]){ //target在mid的右半段
                lo = mid + 1;
            }else{
                hi = mid -1;
            }
        }else{  //左半段是有序的
            if(target >= nums[lo] && target < nums[mid]){ //target 在左半段 
                hi = mid - 1;
            }else{
                lo = mid + 1;
            }
        }
    }
    return -1;
}
```

### 215
[215. 数组中的第K个最大元素](https://leetcode-cn.com/problems/kth-largest-element-in-an-array/)

```html
> 问题描述：
在未排序的数组中找到第 k 个最大的元素。
请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

> 示例：
示例 1:
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5

示例 2:
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

```java
//思路：
//1、我们利用快速排序思想，是查找第 m 小的元素，所以我们这里要转换一下
//2、求数组中的第K个最大元素，实际上就是求数组中的第(nums.length-K+1)个最小元素。
//注意：数组的小标是从0开始的
public int findKthLargest(int[] nums, int k) {
    k = nums.length - k; // k = (nums.length - k +1) - 1
    // nums.length - k +1 表示排好序后的第(nums.length - k +1 )个元素，当前 k 值表示该元素在有序数组中的下标
    int l =0;
    int r= nums.length -1;
    int p=k;
    while(l<=r){
        p = partition(nums,l,r); //p坐标元素的左边都小于 nums[m],右边都大于元素nums[i]
        if( p == k){
           break;
        }else if(p<k){
            l = p+1;
        }else{ // p > k
            assert p>k;
            r = p-1;
        }
    }
    return nums[p];
}

private int partition(int[] nums,int start,int end){
    int pivot = nums[start];
    while(start<end){
        //从右向左遍历，找出第一个<pivot的元素
        while(start<end && nums[end]>=pivot){
            end--;
        }
        nums[start] = nums[end];
        //从左向有遍历，找出第一个>pivot的元素
        while(start<end && nums[start]<=pivot){
            start++;
        }
        nums[end] = nums[start];
    }
    nums[start] = pivot;
    return start;
}
```

### 230
[230. 二叉搜索树中第K小的元素](https://leetcode-cn.com/problems/kth-smallest-element-in-a-bst/)

```html
> 问题描述：
给定一个二叉搜索树，编写一个函数 k thSmallest 来查找其中第 k 个最小的元素。

说明：
你可以假设 k 总是有效的，1 ≤ k ≤ 二叉搜索树元素个数。

> 示例：
示例 1:
输入: root = [3,1,4,null,2], k = 1
   3
  / \
 1   4
  \
   2
输出: 1

示例 2:
输入: root = [5,3,6,2,4,null,null,1], k = 3
       5
      / \
     3   6
    / \
   2   4
  /
 1
输出: 3
```

```java
//思路：利用BST的中序遍历的性质，得到的有序的序列
//写法一：
//空间复杂度：O(n)
public int kthSmallest(TreeNode root, int k) {
    list = new ArrayList<>();
    inOrder(root);
    return list.get(k-1);
}

//存储中序遍历的序列
private List<Integer> list;
private void inOrder(TreeNode root){
    if(root == null){
        return;
    }
    inOrder(root.left);
    list.add(root.val);
    inOrder(root.right);
}
```

```java
//写法二：采用变量记录访问节点数目，这样可以轻松判断是否访问到第k个最小元素
public int kthSmallest(TreeNode root, int k) {
    K = k;
    inOrder(root);
    return res;
}

private int count = 0 ;//统计访问的节点数
private int K = 0; //K表示第k小的元素
private int res = 0 ;
private void inOrder(TreeNode root){
    if(root == null){
        return;
    }
    inOrder(root.left);
    //访问节点
    count++;
    if(K==count){
        res = root.val;
        return;
    }
    inOrder(root.right);
}
```

### 104
[104. 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)
```html
> 问题描述：
给定一个二叉树，找出其最大深度。
二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
说明: 叶子节点是指没有子节点的节点。

> 示例：
给定二叉树 [3,9,20,null,null,15,7]，

    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。
```

```java
public int maxDepth(TreeNode root) {
    if(root==null){
        return 0;
    }
    int leftMaxDepth = maxDepth(root.left);
    int rightMaxDepth = maxDepth(root.right);
    return Math.max(leftMaxDepth,rightMaxDepth)+1;
}
```

### 124
[124. 二叉树中的最大路径和](https://leetcode-cn.com/problems/binary-tree-maximum-path-sum/)

```html
> 问题描述：
给定一个非空二叉树，返回其最大路径和。
本题中，路径被定义为一条从树中任意节点出发，达到任意节点的序列。
该路径至少包含一个节点，且不一定经过根节点。

> 示例：
示例 1:
输入: [1,2,3]

       1
      / \
     2   3
输出: 6

示例 2:
输入: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7
输出: 42
```

```java

```

### 235
[235. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

```html
> 问题描述：
给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。
百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，
满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉搜索树:  root = [6,2,8,0,4,7,9,null,null,3,5]
```
<div align="center"><img src="pics\\bf_1.png" width="400"/></div>

```java

```

### 236
[236. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)

```html
> 问题描述：
给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。
百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，
满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

例如，给定如下二叉树:  root = [3,5,1,6,2,0,8,null,null,7,4]
```
<div align="center"><img src="pics\\bf_2.png" width="400"/></div>

```java

```

## 回溯算法
### 22
[22. 括号生成](https://leetcode-cn.com/problems/generate-parentheses/)

```html
> 问题描述：
给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且有效的括号组合。

例如，给出 n = 3，生成结果为：

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

```java

```

### 78
[78. 子集](https://leetcode-cn.com/problems/subsets/)

```html
> 问题描述：
给定一组不含重复元素的整数数组 nums，返回该数组所有可能的子集（幂集）。

说明：解集不能包含重复的子集。

> 示例:
输入: nums = [1,2,3]
输出:
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

```java

```

### 46
[46. 全排列](https://leetcode-cn.com/problems/permutations/)

```html
> 问题描述：
给定一个没有重复数字的序列，返回其所有可能的全排列。

> 示例:
输入: [1,2,3]
输出:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

```java

```

### 89
[89. 格雷编码](https://leetcode-cn.com/problems/gray-code/)

```html
> 问题描述：
格雷编码是一个二进制数字系统，在该系统中，两个连续的数值仅有一个位数的差异。

给定一个代表编码总位数的非负整数 n，打印其格雷编码序列。格雷编码序列必须以 0 开头。

> 示例：
示例 1:
输入: 2
输出: [0,1,3,2]
解释:
00 - 0
01 - 1
11 - 3
10 - 2
对于给定的 n，其格雷编码序列并不唯一。
例如，[0,2,3,1] 也是一个有效的格雷编码序列。
00 - 0
10 - 2
11 - 3
01 - 1

示例 2:

输入: 0
输出: [0]
解释: 我们定义格雷编码序列必须以 0 开头。
     给定编码总位数为 n 的格雷编码序列，其长度为 2^n。当 n = 0 时，长度为 2^0 = 1。
     因此，当 n = 0 时，其格雷编码序列为 [0]。
```

```java

```


## 动态规划
### 70
[70. 爬楼梯](https://leetcode-cn.com/problems/climbing-stairs/)

```html
> 问题描述：
假设你正在爬楼梯。需要 n 阶你才能到达楼顶。
每次你可以爬 1 或 2 个台阶。你有多少种不同的方法可以爬到楼顶呢？
注意：给定 n 是一个正整数。

> 示例：
示例 1：
输入： 2
输出： 2
解释： 有两种方法可以爬到楼顶。
1.  1 阶 + 1 阶
2.  2 阶

示例 2：
输入： 3
输出： 3
解释： 有三种方法可以爬到楼顶。
1.  1 阶 + 1 阶 + 1 阶
2.  1 阶 + 2 阶
3.  2 阶 + 1 阶
```

```java

```

### 53
[53. 最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

```html
> 问题描述：
给定一个整数数组 nums ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

> 示例:
输入: [-2,1,-3,4,-1,2,1,-5,4],
输出: 6
解释: 连续子数组 [4,-1,2,1] 的和最大，为 6。

> 进阶:
如果你已经实现复杂度为 O(n) 的解法，尝试使用更为精妙的分治法求解。
```

```java

```

### 121
[121. 买卖股票的最佳时机](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock/)

```html
> 问题描述：
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。

如果你最多只允许完成一笔交易（即买入和卖出一支股票），设计一个算法来计算你所能获取的最大利润。

注意你不能在买入股票前卖出股票。

> 示例：
示例 1:
输入: [7,1,5,3,6,4]
输出: 5
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 5 天（股票价格 = 6）的时候卖出，最大利润 = 6-1 = 5 。
     注意利润不能是 7-1 = 6, 因为卖出价格需要大于买入价格。

示例 2:
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

```java

```

### 122
[122. 买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

```html
> 问题描述：
给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。
注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

> 示例：
示例 1:
输入: [7,1,5,3,6,4]
输出: 7
解释: 在第 2 天（股票价格 = 1）的时候买入，在第 3 天（股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     随后，在第 4 天（股票价格 = 3）的时候买入，在第 5 天（股票价格 = 6）的时候卖出, 这笔交易所能获得利润 = 6-3 = 3 。

示例 2:
输入: [1,2,3,4,5]
输出: 4
解释: 在第 1 天（股票价格 = 1）的时候买入，在第 5 天 （股票价格 = 5）的时候卖出, 这笔交易所能获得利润 = 5-1 = 4 。
     注意你不能在第 1 天和第 2 天接连购买股票，之后再将它们卖出。
     因为这样属于同时参与了多笔交易，你必须在再次购买前出售掉之前的股票。

示例 3:
输入: [7,6,4,3,1]
输出: 0
解释: 在这种情况下, 没有交易完成, 所以最大利润为 0。
```

```java

```

### 62
[62. 不同路径](https://leetcode-cn.com/problems/unique-paths/)

```html
> 问题描述：
一个机器人位于一个 m x n 网格的左上角 （起始点在下图中标记为“Start” ）。
机器人每次只能向下或者向右移动一步。机器人试图达到网格的右下角（在下图中标记为“Finish”）。

问总共有多少条不同的路径？

> 说明：
m 和 n 的值均不超过 100。

> 示例：
示例 1:
输入: m = 3, n = 2
输出: 3
解释:
从左上角开始，总共有 3 条路径可以到达右下角。
1. 向右 -> 向右 -> 向下
2. 向右 -> 向下 -> 向右
3. 向下 -> 向右 -> 向右

示例 2:
输入: m = 7, n = 3
输出: 28
```

```java

```

## 设计 
### 146
[146. LRU缓存机制](https://leetcode-cn.com/problems/lru-cache/)

```html
> 问题描述：
运用你所掌握的数据结构，设计和实现一个  LRU (最近最少使用) 缓存机制。
它应该支持以下操作： 获取数据 get 和 写入数据 put 。
获取数据 get(key) - 如果密钥 (key) 存在于缓存中，则获取密钥的值（总是正数），否则返回 -1。
写入数据 put(key, value) - 如果密钥不存在，则写入其数据值。
当缓存容量达到上限时，它应该在写入新数据之前删除最近最少使用的数据值，从而为新的数据值留出空间。

> 进阶:
你是否可以在 O(1) 时间复杂度内完成这两种操作？

> 示例:
LRUCache cache = new LRUCache( 2 /* 缓存容量 */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // 返回  1
cache.put(3, 3);    // 该操作会使得密钥 2 作废
cache.get(2);       // 返回 -1 (未找到)
cache.put(4, 4);    // 该操作会使得密钥 1 作废
cache.get(1);       // 返回 -1 (未找到)
cache.get(3);       // 返回  3
cache.get(4);       // 返回  4
```

```java

```

### 155
[155. 最小栈](https://leetcode-cn.com/problems/min-stack/)

```html
> 问题描述：
设计一个支持 push，pop，top 操作，并能在常数时间内检索到最小元素的栈。

push(x) -- 将元素 x 推入栈中。
pop() -- 删除栈顶的元素。
top() -- 获取栈顶元素。
getMin() -- 检索栈中的最小元素。

> 示例:

MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> 返回 -3.
minStack.pop();
minStack.top();      --> 返回 0.
minStack.getMin();   --> 返回 -2.
```

```java

```