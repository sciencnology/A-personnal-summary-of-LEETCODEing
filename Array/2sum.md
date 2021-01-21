#### [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

难度简单

给定一个整数数组 `nums` 和一个整数目标值 `target`，请你在该数组中找出 **和为目标值** 的那 **两个** 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素不能使用两遍。

你可以按任意顺序返回答案。

 

**示例 1：**

```
输入：nums = [2,7,11,15], target = 9
输出：[0,1]
解释：因为 nums[0] + nums[1] == 9 ，返回 [0, 1] 。
```

**示例 2：**

```
输入：nums = [3,2,4], target = 6
输出：[1,2]
```

**示例 3：**

```
输入：nums = [3,3], target = 6
输出：[0,1]
```

 

**提示：**

- `2 <= nums.length <= 103`
- `-109 <= nums[i] <= 109`
- `-109 <= target <= 109`
- **只会存在一个有效答案**



题目要求返回下标，所以不能先排序再寻找。采用一个HashMap记录每个出现的元素和其下标。遍历数组，对每个元素`num`寻找`targe-num`是否已经存在哈希表中。若未找到则将这个元素插入，否则返回结果

时间复杂度O(N)，空间复杂度O(N)

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        vector<int>result;
        unordered_map<int,int> set;
        int i = -1;
        for(auto num : nums){
            i++;
            if(set.find(target - num) != set.end()){
                result.push_back(i);
                result.push_back(set.find(target - num)->second);
                return result;
            }
            else{
                set.insert({num,i});
            }
        }
        return result;
    }
};
```

