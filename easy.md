## 1 [Two Sum](https://leetcode.com/problems/two-sum/)

###My Solution:

Iterate from the beginning of the vector, use std::find() to search rest of the vector for certain value. If no hits, loop. If hits, push value to return vector.

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        std::vector<int>::iterator it;
        std::vector<int> ret;
        int res;
        for(int i=0;i<nums.size();i++){
            res = target - nums[i];
            it = std::find(nums.begin()+i+1, nums.end(), res);
            if (it == nums.end()) 
                continue; 
            else{
                ret.push_back(i);
                ret.push_back(it-nums.begin());
                return ret;
            }
        }
        return ret;
    }
};
```
Submission Result:

Runtime: 
96 ms, faster than 38.66% of C++ online submissions for Two Sum.

Memory Usage: 9.2 MB, less than 99.18% of C++ online submissions for Two Sum.

###[Disscusion Solution](https://leetcode.com/problems/two-sum/discuss/427020/4ms-C%2B%2B-beats-99.7)
This solution is really fast with only 4ms runtime. Using unordered map for faster value search.
The logic is sligtly different from my solution.
Mine is strait forward, loop the rest part of the vector. 
This solution is looping back, that for each iteration, search all pairs within the map.

```
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> m;
        vector<int> res;
        
        for(int i = 0; i < nums.size() ; i++){
            if(m.count(target - nums[i]) != 0) res = {i, m[target-nums[i]]};
            m[nums[i]] = i;                                             
        }
        return res;
    }
};
```