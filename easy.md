## 1 - [Two Sum](https://leetcode.com/problems/two-sum/)

### My Solution: 96 ms   9.2 MB

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

### [Disscusion Solution](https://leetcode.com/problems/two-sum/discuss/427020/4ms-C%2B%2B-beats-99.7)

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


## 566 - [Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/)

### My Solution: 36 ms   12.2 MB
1. If the size of matrix is not equal, return original.
2. Create row-traversing vector.
3. Assign value to new matrix.

```
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) {
        int i,j;
        
        int row = nums.size();
        int col = nums[0].size();
        
        if((row*col)!=(r*c)) return nums;
        
        vector<int> rowt;
        for(i=0;i<row;i++){
            for(j=0;j<col;j++){
                rowt.push_back(nums[i][j]);
            }
        }
        vector<vector<int>> ret(r,vector<int>(c));
        for(i=0;i<r;i++){
            for(j=0;j<c;j++){
                ret[i][j] = rowt[i*c+j];
            }
        }
        return ret;
    }
};
```

### Faster Solution: 24 ms
Really smart.

```
class Solution {
public:
    vector<vector<int>> matrixReshape(vector<vector<int>>& nums, int r, int c) {
        vector<vector<int>> ans;
        vector<int> trav;
        
        int nRows = nums.size();
        int nCols = nums[0].size();
        if (r * c != nRows * nCols)
            return nums;
        
        for (int a = 0; a < nRows; a++){
            for (int b = 0; b < nCols; b++){
                trav.push_back(nums[a][b]);
            }
        }
        
        vector<int> temp;
        int j = 0;
        for (auto i : trav){
            temp.push_back(i);
            j++;
            
            if (j == c){
                ans.push_back(temp);
                temp.clear();
                j = 0;
            }
        }
        return ans;
    }
};
```