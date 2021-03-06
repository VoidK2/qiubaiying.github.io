---
layout:  post
title: leetcode刷题
subtitle: 记录
date: 2021-2-26
author: zhangzexin
header-img: img/post-bg-unix-linux.jpg
catalog: true
tags:
- leetcode
- java
---

## 1178.[猜字谜](https://leetcode-cn.com/problems/number-of-valid-words-for-each-puzzle/)

```java
class Solution {
    public List<Integer> findNumOfValidWords(String[] words, String[] puzzles) {
        HashMap<Integer,Integer> map = new HashMap<>();
        for(String word:words){
            int mask=getBit(word);
            if(Integer.bitCount(mask)<=7){
                map.put(mask,map.getOrDefault(mask,0)+1);
            }
        }
        List<Integer> ans = new ArrayList<>();
        for(String puzzle:puzzles){
            int cnt=0;
            int first=getBit(puzzle.substring(0,1));
            int mask=getBit(puzzle.substring(1));
            int subset=mask;
            while(subset!=0){
                int key=first|subset;
                if(map.containsKey(key)){
                    cnt+=map.get(key);
                }
                subset=(subset-1)&mask;
            }
            if(map.containsKey(first)){
                cnt+=map.get(first);
            }
            ans.add(cnt);
        }
        return ans;
    }
    private int getBit(String word){
        int mask=0;
        for(int i = 0; i < word.length(); i++){
            char ch=word.charAt(i);
            mask |=( 1 << ( ch - 'a' ));
        }
        return mask;
    }
}
```

## 1.[两数之和](https://leetcode-cn.com/problems/two-sum/)

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] ans = new int[2];
        label1:for(int i=0;i<nums.length;i++){
            for(int j=i+1;j<nums.length;j++){
                if(nums[i]+nums[j]==target){
                    ans[0]=i;
                    ans[1]=j;
                    break label1;
                }
            }
        }
        return ans;
    }
}
```

## 2.[两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int a1=0,a2=0,a3=0,tmp=0,times=1;
        ListNode l3=new ListNode();
        ListNode l4=l3;
        while(l1!=null||l2!=null||tmp!=0){
            int x=l1==null?0:l1.val;
            int y=l2==null?0:l2.val;
            int sum=x+y+tmp;
            tmp=sum/10;
            l4.next=new ListNode(sum%10);
            l4=l4.next;
            if(l1!=null){
                l1=l1.next;
            }
            if(l2!=null){
                l2=l2.next;
            }
        }
        return l3.next;
    }
}
```

## 201.[数字范围按位与](https://leetcode-cn.com/problems/bitwise-and-of-numbers-range/)

```java
class Solution {
    public int rangeBitwiseAnd(int left, int right) {
        if(right==0){
            return 0;
        }
        int i=0;
        while(left!=right){
            left=left>>1;
            right=right>>1;
            i++;
        }
        return left<<i;
    }
}
```


## 82.[删除排序链表中的重复元素 II](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii/)

```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null){
            return head;
        }
        int flag=0;
        ListNode head2 = new ListNode(0,head);
        ListNode head3=head2;

        while(head3.next!=null&&head3.next.next!=null){
            if(head3.next.val==head3.next.next.val){
                flag=head3.next.val;
                while(head3.next!=null&&head3.next.val==flag){
                    head3.next=head3.next.next;
                }
            }else{
                head3=head3.next;
            }
        }
        return head2.next;
    }
}
```

## 83.[删除排序链表中的重复元素](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list/)
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head==null){
            return head;
        }
        int flag=0;
        ListNode head2 = new ListNode(0,head);
        ListNode head3=head2;

        while(head3.next!=null&&head3.next.next!=null){
            if(head3.next.val==head3.next.next.val){
                flag=head3.next.val;
                while(head3.next.next!=null&&head3.next.next.val==flag){
                    head3.next=head3.next.next;
                }
            }else{
                head3=head3.next;
            }
        }
        return head2.next;
    }
}
```

## 456.[132 模式](https://leetcode-cn.com/problems/132-pattern/)
```java
class Solution {
    public boolean find132pattern(int[] nums) {
        if(nums.length<3){
            return false;
        }
        int min=nums[0];
        for(int i=0;i<nums.length;i++){
            min=Math.min(min,nums[i]);
            if(min==nums[i]){
                continue;
            }
            for(int j=nums.length-1;j>i;j--){
                if(min<nums[j]&&nums[j]<nums[i]){
                    return true;
                }
            }
        }
        return false;
    }
}
```

## 191.[位1的个数](https://leetcode-cn.com/problems/number-of-1-bits/)
```java
public class Solution {
    // you need to treat n as an unsigned value
    public int hammingWeight(int n) {
        int ans=0;
        for(int i=0;i<32;i++){
            if((n&(1<<i))!=0){
                ans++;
            }
        }
        return ans;
    }
}
```


## 73.[矩阵置零](https://leetcode-cn.com/problems/set-matrix-zeroes/)
```java
class Solution {
    public void setZeroes(int[][] matrix) {
        int m=matrix.length;
        int n=matrix[0].length;
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==0){
                    for(int k=0;k<n;k++){
                        if(matrix[i][k]!=0){
                            matrix[i][k]=9999;
                        }
                    }
                    for(int x=0;x<m;x++){
                        if(matrix[x][j]!=0){
                            matrix[x][j]=9999;
                        }
                    }
                }
            }
        }
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(matrix[i][j]==9999){
                    matrix[i][j]=0;
                }
            }
        }
    }
}
```

## 150.[逆波兰表达式求值](https://leetcode-cn.com/problems/evaluate-reverse-polish-notation/)
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Deque<Integer> stack = new LinkedList<Integer>();
        int n = tokens.length;
        for (int i = 0; i < n; i++) {
            String token = tokens[i];
            if (isNumber(token)) {
                stack.push(Integer.parseInt(token));
            } else {
                int num2 = stack.pop();
                int num1 = stack.pop();
                switch (token) {
                    case "+":
                        stack.push(num1 + num2);
                        break;
                    case "-":
                        stack.push(num1 - num2);
                        break;
                    case "*":
                        stack.push(num1 * num2);
                        break;
                    case "/":
                        stack.push(num1 / num2);
                        break;
                    default:
                }
            }
        }
        return stack.pop();
    }

    public boolean isNumber(String token) {
        return !("+".equals(token) || "-".equals(token) || "*".equals(token) || "/".equals(token));
    }
}

```

## 1603.[设计停车系统](https://leetcode-cn.com/problems/design-parking-system/)
```java
class ParkingSystem {
    int big,medium,small;
    public ParkingSystem(int big, int medium, int small) {
        this.big=big;
        this.medium=medium;
        this.small=small;
    }
    
    public boolean addCar(int carType) {
        if(carType==1&&big>0){
            big--;
            return true;
        }else if(carType==2&&medium>0){
            medium--;
            return true;
        }else if(carType==3&&small>0){
            small--;
            return true;
        }else{
            return false;
        }
    }
}

/**
 * Your ParkingSystem object will be instantiated and called as such:
 * ParkingSystem obj = new ParkingSystem(big, medium, small);
 * boolean param_1 = obj.addCar(carType);
 */
```

## 208.[实现 Trie (前缀树)](https://leetcode-cn.com/problems/implement-trie-prefix-tree/)
```java
class Trie {
        Trie[] next = new Trie[26];
        boolean isEnd = false;

        public Trie() {
        }

        public void insert(String word) {
            Trie curr = this;
            for (char c : word.toCharArray()) {
                if (curr.next[c - 'a'] == null) {
                    curr.next[c - 'a'] = new Trie();
                }
                curr = curr.next[c - 'a'];
            }
            curr.isEnd = true;
        }

        public boolean search(String word) {
            Trie curr = this;
            for (char c : word.toCharArray()) {
                if (curr.next[c - 'a'] == null) return false;
                curr = curr.next[c - 'a'];
            }
            return curr.isEnd;
        }
   
        public boolean startsWith(String prefix) {
            Trie curr = this;
            for (char c : prefix.toCharArray()) {
                if (curr.next[c - 'a'] == null) return false;
                curr = curr.next[c - 'a'];
            }
            return true;
        }
    }

```
