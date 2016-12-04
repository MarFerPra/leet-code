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

#### Palindrome Number

Determine whether an integer is a palindrome. Do this without extra space.

```
public class Solution {
    public boolean isPalindrome(int x) {

        int digits = String.valueOf(x).length();

        if(x < 0) return false;

        if(digits == 1) return true;

        int secondHalf = 0;  

        for(int i = 0; i < digits/2; i++){
            secondHalf *= 10;
            secondHalf += x%10;
            x /= 10;
        }

        if(digits%2 != 0){
            x /= 10;
        }

        return(secondHalf == x);

    }
}
```


#### Palindrome Linked List

Given a singly linked list, determine if it is a palindrome. ( In O(n) time and O(1) space )

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public boolean isPalindrome(ListNode head) {

            if(head == null || head.next == null) return true;

            ListNode slow_ptr = head;
            ListNode previous_to_slow = head;
            ListNode fast_ptr = head;
            ListNode midpoint;

            while(fast_ptr != null && fast_ptr.next != null){
                fast_ptr = fast_ptr.next.next;
                previous_to_slow = slow_ptr;
                slow_ptr = slow_ptr.next;

            }

            previous_to_slow.next = null;

            /* If fast_ptr not null means its odd number of elements, remove midpoint. */
            if(fast_ptr != null){
                midpoint = slow_ptr;
                slow_ptr = slow_ptr.next;
            }

            /* Inverse second half, using slow_ptr as aux variable. */
            ListNode previous = null;
            ListNode current = slow_ptr;
            ListNode next;

            while(current != null){
                next = current.next;
                current.next = previous;
                previous = current;
                current = next;
            }

            /* Compare first half with second half */

            ListNode firstHalf = head;
            ListNode secondHalf = previous;

            while(firstHalf != null && secondHalf != null){
                if(firstHalf.val != secondHalf.val) return false;
                firstHalf = firstHalf.next;
                secondHalf = secondHalf.next;
            }

            return true;
    }
}
```


#### Reverse Linked List

Reverse a singly linked list.

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    public ListNode reverseList(ListNode head) {
        ListNode previous = null;
        ListNode current = head;
        ListNode next;

        while(current != null){
            next = current.next;  
            current.next = previous;
            previous = current;
            current = next;
        }

        return previous;
    }
}
```
