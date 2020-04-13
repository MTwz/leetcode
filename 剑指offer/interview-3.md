# 数组中重复的数字

+ https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/submissions/

## 解法：
    - 桶排序：
    ```java
    public int findRepeatNumber(int[] nums) {
        int[] bucket = new int[nums.length];
        int length  = nums.length;
        for(int i = 0; i < length; i++){
            if(bucket[nums[i]] == 0){
                bucket[nums[i]]++;
            } else{
                return nums[i];
            }
            
        }
        return -1;
    }
    ```
    - 基于交换：“如果数组中没有重复的数字，那么当数组重新排序后数字i将在下标为i的位置”
    ``` java
    public int findRepeatNumber(int[] nums) {
            int swap = -1;
            int idx = 0;
            while(idx<nums.length){
                if(nums[idx] == idx){
                    idx++;
                }else{//注意：idx不变，持续进行交换，直到发现相重或者nums[idx] == idx
                    swap = nums[nums[idx]];
                    if(swap == nums[idx]){
                        return swap;
                    }
                    nums[nums[idx]] = nums[idx];
                    nums[idx] = swap;
                }
                
            }
            return -1;
        }
    ```