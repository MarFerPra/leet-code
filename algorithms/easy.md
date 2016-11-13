##### String to Integer (atoi)

```
public class Solution {
    public int myAtoi(String str) {
        if (str.isEmpty()) return 0;

        int sol = 0, index = 0;
        boolean negative = false;
        char[] input = str.toCharArray();
        int sumRes = 0;
        int maxValue = Integer.MAX_VALUE/10;

        while(Character.isWhitespace(input[index])) { // Whitespaces
            index++;
            if (index == input.length) return 0; // Just whitespaces
        }
        if (input[index] == '-') { // Negative
            index++;
            negative = true;
        }
        else if (input[index] == '+') index++; // Positive

        for (int i = index; i < input.length; i++) {
            if (Character.isDigit(input[i])){

              sumRes = sol*10 + Character.getNumericValue(input[i]);

              if( sol > maxValue || sol > sumRes ){
                if(negative)
                  return Integer.MIN_VALUE;
                else
                  return Integer.MAX_VALUE;
              } else {
                sol = sumRes;
              }
            }

            else if (sol == 0) return 0;
            else break;
        }

        if (negative) sol = 0 - sol;

        return sol;
    }
}
```

##### Two Sum
Given an array of integers, return index of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution.

```
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```
