# leetcode题解

## 1. 两数之和
给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

    class Solution {
        public int[] twoSum(int[] nums, int target) {
            for(int i = 0; i < nums.length - 1; i++){
                for(int j = i+1; j < nums.length; j++) {
                    if((nums[i] + nums[j]) == target) {
                        return new int[]{i, j};
                    }
                }
            }
            return new int[0];
        }
    }

## 2. 两数相加
给你两个 非空 的链表，表示两个非负的整数。它们每位数字都是按照 逆序 的方式存储的，并且每个节点只能存储 一位 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

![](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/01/02/addtwonumber1.jpg)

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
            int one = (l1.val + l2.val)/10;
            ListNode l3 = new ListNode((l1.val + l2.val)%10);
            ListNode head = l3;
            ListNode next = null;
            while(l1.next != null && l2.next != null) {
                l2 = l2.next;
                l1 = l1.next;
                next = new ListNode((l1.val + l2.val + one)%10);
                one = (l1.val + l2.val + one)/10;
                l3.next = next;
                l3 = next;
            }

            if(l1.next == null) {
                while(l2.next != null) {
                    l2 = l2.next;
                    next = new ListNode((l2.val + one)%10);
                    one = (one + l2.val)/10;
                    l3.next = next;
                    l3 = next;
                }
            }

            if(l2.next == null) {
                while(l1.next != null) {
                    l1 = l1.next;
                    next = new ListNode((l1.val + one)%10);
                    one = (one + l1.val)/10;
                    l3.next = next;
                    l3 = next;
                }
            }
            if(one == 1) {
                next = new ListNode(1);
                l3.next = next;
                next.next = null;
            }
            return head;
        }
    }