
## 2023/06/19

### Question 1
https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/

Given an integer array nums sorted in non-decreasing order, remove some duplicates in-place such that each unique element appears at most twice. The relative order of the elements should be kept the same.

Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

Initial Solution
```java
class Solution {
    public int removeDuplicates(int[] nums) {
        // boolean hitDuplicateMax = true;
        int indexToFill = 0;
        int allowedDuplicate = 2;
        int previous = nums[0];
        
        int uniqueCount = 0;
        for(int i = 0; i < nums.length; i++){
            if(allowedDuplicate == 0){
                // // Current duplicate has reached maximum count
                // if(hitDuplicateMax){
                //     hitDuplicateMax = false;
                //     indexToFill = i;
                // }
                
                if(nums[i] != previous){
                    // current number isn't a duplicate
                    // The initial value needs to be 1
                    allowedDuplicate = 1;
                    nums[indexToFill++] = nums[i];
                    uniqueCount++;
                } else {
                    // current number is a duplicate
                }
            } else {
                if(nums[i] == previous){
                    // Current number is a duplicate
                    allowedDuplicate--;
                    uniqueCount++;
                    
                } else {
                    // Current number isn't a duplicate
                    
                    uniqueCount++;
                }
                   nums[indexToFill++] = nums[i];
            }
            previous = nums[i];
        }
        
        return uniqueCount;
        
    }
}
```

Improved solution:
Remove redundant parameter previous & uniqueCount
Overwrite values that we don't want, and return the pointer index


```java
class Solution {
    public int removeDuplicates(int[] nums) {
        // boolean hitDuplicateMax = true;
        int indexToFill = 1;
        int allowedDuplicate = 1;
      
        
     //   int uniqueCount = 1;
        for(int i = 1; i < nums.length; i++){
            
             if(nums[i] == nums[i-1]){
                    // Current number is a duplicate
                    allowedDuplicate--;
                    
             } else {
                 // current number isn't a duplicate
                    // The initial value needs to be 1
                   allowedDuplicate = 1;
                    // nums[indexToFill++] = nums[i];
                    // uniqueCount++;
             }
            
            
            if(allowedDuplicate >= 0){
                  nums[indexToFill++] = nums[i];
            }
        
          
        }
        
        return indexToFill;
        
    }
}
```
Time O(1) Space O(N)

![image](https://github.com/pagexv/leetcode-Team/assets/33244427/0c9898e0-2982-4b43-a2ae-8604e87e6444)