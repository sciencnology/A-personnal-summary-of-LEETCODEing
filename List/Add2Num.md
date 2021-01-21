#### [2. 两数相加](https://leetcode-cn.com/problems/add-two-numbers/)

难度中等

给你两个 **非空** 的链表，表示两个非负的整数。它们每位数字都是按照 **逆序** 的方式存储的，并且每个节点只能存储 **一位** 数字。

请你将两个数相加，并以相同形式返回一个表示和的链表。

你可以假设除了数字 0 之外，这两个数都不会以 0 开头。

 

**示例 1：**

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2021/01/02/addtwonumber1.jpg)

```
输入：l1 = [2,4,3], l2 = [5,6,4]
输出：[7,0,8]
解释：342 + 465 = 807.
```

**示例 2：**

```
输入：l1 = [0], l2 = [0]
输出：[0]
```

**示例 3：**

```
输入：l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
输出：[8,9,9,9,0,0,0,1]
```

 

**提示：**

- 每个链表中的节点数在范围 `[1, 100]` 内
- `0 <= Node.val <= 9`
- 题目数据保证列表表示的数字不含前导零



模拟小学生计算加法过程，设置一个整数c表示进位，每次讲两个链表相应位置和c相加得到结果的某位数字，并加到结果链表上。当两个链表都加完后，继续判断进位c是否为1决定是否需要最后补上进位1（惨痛样例**[9,9,9,9,9,9,9] [9,9,9,9]**）

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        int c = 0;//表示进位
        ListNode* p = l1,* q = l2;
        ListNode* res = new ListNode, * r = res;
        while(p || q){
            int pv = (p)?(p->val):0;
            int qv = (q)?(q->val):0;
            int val = pv + qv + c;
            if(val >= 10){
                val -= 10;
                c = 1;
            }
            else c = 0;
            ListNode* m = new ListNode(val);
            r->next = m;
            r = m;
            p = (!p)?p:p->next;
            q = (!q)?q:q->next;
        }
        if(c){
            ListNode* m = new ListNode(1);
            r->next = m;
            r = m;
        }
        return res->next;
    }
};
```

